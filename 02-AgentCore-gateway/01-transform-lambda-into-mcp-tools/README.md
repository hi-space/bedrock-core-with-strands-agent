# Gateway용 Lambda 함수 도구 구현

## 개요
Bedrock AgentCore Gateway는 고객이 인프라나 호스팅을 관리할 필요 없이 기존 Lambda 함수를 완전 관리형 MCP 서버로 전환할 수 있는 방법을 제공합니다. 고객은 기존 AWS Lambda 함수를 가져오거나 도구를 프론트하는 새로운 Lambda 함수를 추가할 수 있습니다. Gateway는 이러한 모든 도구에 걸쳐 통일된 Model Context Protocol(MCP) 인터페이스를 제공합니다. Gateway는 들어오는 요청과 대상 리소스에 대한 아웃바운드 연결 모두에 대해 안전한 액세스 제어를 보장하기 위해 이중 인증 모델을 사용합니다. 프레임워크는 두 가지 주요 구성 요소로 구성됩니다: 게이트웨이 대상에 액세스하려는 사용자를 검증하고 권한을 부여하는 Inbound Auth와 인증된 사용자를 대신하여 게이트웨이가 백엔드 리소스에 안전하게 연결할 수 있도록 하는 Outbound Auth입니다. 이러한 인증 메커니즘은 함께 사용자와 대상 리소스 간의 안전한 브리지를 만들어 IAM 자격 증명과 OAuth 기반 인증 플로우를 모두 지원합니다.

![작동 방식](images/lambda-iam-gateway.png)

### Lambda 컨텍스트 객체 이해
Gateway가 Lambda 함수를 호출할 때 context.client_context 객체를 통해 특별한 컨텍스트 정보를 전달합니다. 이 컨텍스트에는 호출에 대한 중요한 메타데이터가 포함되어 있으며, 함수가 요청을 처리하는 방법을 결정하는 데 사용할 수 있습니다.
context.client_context.custom 객체에서 다음 속성을 사용할 수 있습니다:
* bedrockagentcoreEndpointId: 요청을 받은 Gateway 엔드포인트의 ID입니다.
* bedrockagentcoreTargetId: 요청을 함수로 라우팅한 Gateway 대상의 ID입니다.
* bedrockagentcoreMessageVersion: 요청에 사용된 메시지 형식의 버전입니다.
* bedrockagentcoreToolName: 호출되는 도구의 이름입니다. Lambda 함수가 여러 도구를 구현할 때 특히 중요합니다.
* bedrockagentcoreSessionId: 현재 호출의 세션 ID로, 동일한 세션 내에서 여러 도구 호출을 연관시키는 데 사용할 수 있습니다.

Lambda 함수 코드에서 이러한 속성에 액세스하여 어떤 도구가 호출되는지 확인하고 그에 따라 함수의 동작을 사용자 정의할 수 있습니다.

![작동 방식](images/lambda-context-object.png)

### 응답 형식 및 오류 처리

Lambda 함수는 Gateway가 해석하고 클라이언트에 다시 전달할 수 있는 응답을 반환해야 합니다. 응답은 다음 구조를 가진 JSON 객체여야 합니다. statusCode 필드는 작업 결과를 나타내는 HTTP 상태 코드여야 합니다:
* 200: 성공
* 400: 잘못된 요청 (클라이언트 오류)
* 500: 내부 서버 오류

body 필드는 문자열이거나 더 복잡한 응답을 나타내는 JSON 문자열일 수 있습니다. 구조화된 응답을 반환하려면 JSON 문자열로 직렬화해야 합니다.

### 오류 처리
적절한 오류 처리는 클라이언트에 의미 있는 피드백을 제공하는 데 중요합니다. Lambda 함수는 예외를 포착하고 적절한 오류 응답을 반환해야 합니다.

### 테스트

```__context__``` 필드는 Gateway에서 호출될 때 함수에 전달되는 실제 이벤트의 일부가 아닙니다. 컨텍스트 객체를 시뮬레이션하기 위한 테스트 목적으로만 사용됩니다.
Lambda 콘솔에서 테스트할 때 시뮬레이션된 컨텍스트를 처리하도록 함수를 수정해야 합니다. 이 접근 방식을 통해 Lambda 함수를 Gateway 대상으로 배포하기 전에 다양한 도구 이름과 입력 매개변수로 테스트할 수 있습니다.

### 교차 계정 Lambda 액세스

Lambda 함수가 Gateway와 다른 AWS 계정에 있는 경우 Gateway가 함수를 호출할 수 있도록 Lambda 함수에 리소스 기반 정책을 구성해야 합니다. 다음은 예제 정책입니다:

```
{
  "Version": "2012-10-17",
  "Id": "default",
  "Statement": [
    {
      "Sid": "cross-account-access",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::123456789012:role/GatewayExecutionRole"
      },
      "Action": "lambda:InvokeFunction",
      "Resource": "arn:aws:lambda:us-west-2:987654321098:function:MyLambdaFunction"
    }
  ]
}
```
이 정책에서:
- 123456789012는 Gateway가 배포된 계정 ID입니다
- GatewayExecutionRole은 Gateway에서 사용하는 IAM 역할입니다.
- 987654321098은 Lambda 함수가 배포된 계정 ID입니다.
- MyLambdaFunction은 Lambda 함수의 이름입니다.

이 정책을 추가한 후 다른 계정에 있더라도 Gateway 대상 구성에서 Lambda 함수 ARN을 지정할 수 있습니다.

### 튜토리얼 세부 정보

| 정보          | 세부 사항                                                   |
|:---------------------|:----------------------------------------------------------|
| 튜토리얼 유형        | 대화형                                               |
| AgentCore 구성 요소 | AgentCore Gateway, AgentCore Identity                     |
| 에이전트 프레임워크    | Strands Agents                                            |
| LLM 모델            | Anthropic Claude Sonnet 3.7, Amazon Nova Pro              |
| 튜토리얼 구성 요소  | AgentCore Gateway 생성 및 AgentCore Gateway 호출 |
| 튜토리얼 분야    | 교차 분야                                            |
| 예제 복잡성   | 쉬움                                                      |
| 사용된 SDK             | boto3                                                     |

## 튜토리얼 아키텍처

### 튜토리얼 주요 기능

* Lambda 함수를 MCP 도구로 노출
* AWS IAM 및 OAuth를 사용하여 도구 호출 보안

## 튜토리얼 개요

이 튜토리얼에서는 다음 기능을 다룹니다:

- [AWS Lambda 함수를 MCP 도구로 변환](01-gateway-target-lambda.ipynb)

