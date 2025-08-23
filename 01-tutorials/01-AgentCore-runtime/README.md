# Amazon Bedrock AgentCore Runtime

## 개요
Amazon Bedrock AgentCore Runtime은 AI 에이전트와 도구를 배포하고 확장하기 위해 설계된 안전하고 서버리스 런타임입니다. 
모든 프레임워크, 모델 및 프로토콜을 지원하여 개발자가 최소한의 코드 변경으로 로컬 프로토타입을 프로덕션 준비 솔루션으로 변환할 수 있도록 합니다.

Amazon BedrockAgentCore Python SDK는 에이전트 함수를 Amazon Bedrock과 호환되는 HTTP 서비스로 배포하는 데 도움이 되는 경량 래퍼를 제공합니다. 모든 HTTP 서버 세부 사항을 처리하므로 에이전트의 핵심 기능에 집중할 수 있습니다.

`@app.entrypoint` 데코레이터로 함수를 장식하고 SDK의 `configure` 및 `launch` 기능을 사용하여 에이전트를 AgentCore Runtime에 배포하기만 하면 됩니다. 그러면 애플리케이션이 SDK 또는 boto3, AWS SDK for JavaScript 또는 AWS SDK for Java와 같은 AWS 개발자 도구를 사용하여 이 에이전트를 호출할 수 있습니다.

![Runtime 개요](images/runtime_overview.png)

## 주요 기능

### 프레임워크 및 모델 유연성

- 모든 프레임워크(Strands Agents, LangChain, LangGraph, CrewAI 등)에서 에이전트와 도구 배포
- 모든 모델 사용(Amazon Bedrock 내외 모델)

### 통합

Amazon Bedrock AgentCore Runtime은 통합 SDK를 통해 다른 Amazon Bedrock AgentCore 기능과 통합됩니다:

- Amazon Bedrock AgentCore Memory
- Amazon Bedrock AgentCore Gateway
- Amazon Bedrock AgentCore Observability
- Amazon Bedrock AgentCore Tools

이러한 통합은 개발 프로세스를 단순화하고 AI 에이전트를 구축, 배포 및 관리하기 위한 포괄적인 플랫폼을 제공하는 것을 목표로 합니다.

### 사용 사례

런타임은 다음을 포함한 광범위한 애플리케이션에 적합합니다:

- 실시간 대화형 AI 에이전트
- 장기 실행되는 복잡한 AI 워크플로
- 멀티모달 AI 처리(텍스트, 이미지, 오디오, 비디오)

## 튜토리얼 개요

이 튜토리얼에서는 다음 기능을 다룹니다:

- [에이전트 호스팅](01-hosting-agent)
- [MCP 서버 호스팅](02-hosting-MCP-server)
- [고급 개념](03-advanced-concepts)

