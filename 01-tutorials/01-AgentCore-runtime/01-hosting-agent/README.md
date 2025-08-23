# AgentCore Runtime에서 AI 에이전트 호스팅

## 개요

이 튜토리얼은 Amazon Bedrock AgentCore Python SDK를 사용하여 **Amazon Bedrock AgentCore Runtime**에서 AI 에이전트를 호스팅하는 방법을 보여줍니다. 에이전트 코드를 Amazon Bedrock의 인프라와 원활하게 통합되는 표준화된 HTTP 서비스로 변환하는 방법을 학습합니다.

AgentCore Runtime은 모든 에이전트 프레임워크(Strands Agents, LangGraph, CrewAI)와 모든 LLM 모델(Amazon Bedrock, OpenAI 등)로 구축된 에이전트를 호스팅할 수 있는 **프레임워크 및 모델 독립적** 플랫폼입니다.

Amazon Bedrock AgentCore Python SDK는 다음과 같은 래퍼 역할을 합니다:

- 에이전트 코드를 AgentCore의 표준화된 프로토콜로 **변환**
- HTTP 및 MCP 서버 인프라를 자동으로 **처리**
- 에이전트의 핵심 기능에 **집중**할 수 있도록 지원
- 두 가지 프로토콜 유형 **지원**:
  - **HTTP 프로토콜**: 전통적인 요청/응답 REST API 엔드포인트
  - **MCP 프로토콜**: 도구 및 에이전트 서버를 위한 Model Context Protocol

### 서비스 아키텍처

에이전트를 호스팅할 때 SDK는 자동으로:

- 포트 `8080`에서 에이전트 호스팅
- 두 가지 주요 엔드포인트 제공:
  - **`/invocations`**: 주요 에이전트 상호 작용 (JSON 입력 → JSON/SSE 출력)
  - **`/ping`**: 모니터링을 위한 상태 확인

![에이전트 호스팅](images/hosting_agent_python_sdk.png)

에이전트가 AgentCore Runtime에 배포할 준비가 되면 Amazon Bedrock AgentCore StarterKit을 사용하여 AgentCore Runtime에 배포할 수 있습니다.

StarterKit을 사용하면 에이전트 배포를 구성하고 실행하여 에이전트 구성과 AgentCore Runtime 엔드포인트가 포함된 Amazon ECR 저장소를 생성하고 검증을 위해 생성된 엔드포인트를 호출할 수 있습니다.

![StarterKit](../images/runtime_overview.png)

배포되면 AWS의 AgentCore Runtime 아키텍처는 다음과 같습니다:

![Runtime 아키텍처](../images/runtime_architecture.png)

## 튜토리얼 예제

이 튜토리얼에는 시작하는 데 도움이 되는 세 가지 실습 예제가 포함되어 있습니다:

| 예제                                                                | 프레임워크      | 모델          | 설명                                |
| ---------------------------------------------------------------------- | -------------- | -------------- | ------------------------------------------ |
| **[01-strands-with-bedrock-model](01-strands-with-bedrock-model)**     | Strands Agents | Amazon Bedrock | AWS 네이티브 모델을 사용한 기본 에이전트 호스팅 |
| **[02-langgraph-with-bedrock-model](02-langgraph-with-bedrock-model)** | LangGraph      | Amazon Bedrock | LangGraph 에이전트 워크플로                  |
| **[03-strands-with-openai-model](03-strands-with-openai-model)**       | Strands Agents | OpenAI         | 외부 LLM 공급자와의 통합    |

## 주요 이점

- **프레임워크 독립적**: 모든 Python 기반 에이전트 프레임워크와 작동
- **모델 유연성**: Amazon Bedrock, OpenAI 및 기타 LLM 공급자의 LLM 지원
- **프로덕션 준비**: 내장 상태 확인 및 모니터링
- **쉬운 통합**: 최소한의 코드 변경 필요
- **확장 가능**: 엔터프라이즈 워크로드를 위해 설계

## 시작하기

선호하는 프레임워크와 모델 조합에 따라 위의 튜토리얼 예제 중 하나를 선택하세요. 각 예제에는 다음이 포함됩니다:

- 단계별 설정 지침
- 완전한 코드 샘플
- 테스트 가이드라인
- 모범 사례

## 다음 단계

튜토리얼을 완료한 후 다음을 수행할 수 있습니다:

- 이러한 패턴을 다른 프레임워크와 모델로 확장
- 프로덕션 환경에 배포
- 기존 애플리케이션과 통합
- 에이전트 인프라 확장
