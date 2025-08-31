# Amazon AgentCore Bedrock Code Interpreter를 사용한 에이전트 기반 코드 실행 - 튜토리얼

## 개요

이 튜토리얼은 Python을 사용한 코드 실행을 통해 답변을 검증하는 AI 에이전트를 만드는 방법을 보여줍니다. Amazon Bedrock AgentCore Code Interpreter를 사용하여 LLM에서 생성된 코드를 실행합니다.

이 튜토리얼은 Amazon Bedrock AgentCore Code Interpreter를 사용하여 다음을 수행하는 방법을 보여줍니다:

1. 샌드박스 환경 설정
2. 사용자 쿼리를 기반으로 코드를 생성하는 strands 및 langchain 기반 에이전트 구성
3. Code Interpreter를 사용하여 샌드박스 환경에서 코드 실행
4. 결과를 사용자에게 다시 표시

### 튜토리얼 세부 정보

| 정보         | 세부 사항                                                                          |
|:--------------------|:---------------------------------------------------------------------------------|
| 튜토리얼 유형       | 대화형                                                                   |
| 에이전트 유형          | 단일                                                                           |
| 에이전트 프레임워크   | Langchain & Strands Agents                                                       |
| LLM 모델           | Anthropic Claude Sonnet 3.5 & 3.7                                                |
| 튜토리얼 구성 요소 | Amazon Bedrock AgentCore Code Interpreter                                                        |
| 튜토리얼 분야   | 교차 분야                                                                   |
| 예제 복잡성  | 쉬움                                                                             |
| 사용된 SDK            | Amazon BedrockAgentCore Python SDK 및 boto3                                     |

### 튜토리얼 아키텍처

코드 실행 샌드박스는 코드 인터프리터, 셸 및 파일 시스템이 있는 격리된 환경을 생성하여 에이전트가 사용자 쿼리를 안전하게 처리할 수 있도록 합니다. 대규모 언어 모델이 도구 선택을 도운 후 이 세션 내에서 코드가 실행되고 합성을 위해 사용자 또는 에이전트에게 반환됩니다.

<div style="text-align:left">
    <img src="images/code_interpreter.png" width="100%"/>
</div>
