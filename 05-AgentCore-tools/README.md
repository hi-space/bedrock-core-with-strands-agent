# Amazon Bedrock AgentCore Tools

## 개요
Amazon Bedrock AgentCore Tools는 AI 에이전트가 복잡한 작업을 안전하고 효율적으로 수행할 수 있는 능력을 향상시키는 엔터프라이즈급 기능을 제공합니다. 이 도구 모음에는 두 가지 주요 도구가 포함됩니다:

- Amazon Bedrock AgentCore Code Interpreter 및
- Amazon Bedrock AgentCore Browser Tool

## Amazon Bedrock AgentCore Code Interpreter

### 주요 기능

1. **안전한 코드 실행**: 격리된 샌드박스 환경에서 코드를 실행하여 내부 데이터 소스에 액세스하면서 보안을 보장합니다.

2. **완전 관리형 AWS 네이티브 솔루션**: Strands Agents, LangGraph, CrewAI와 같은 프레임워크와 원활하게 통합됩니다.

3. **고급 구성 지원**: 입력 및 출력 모두에 대한 대용량 파일 지원과 인터넷 액세스를 포함합니다.

4. **다중 언어 지원**: JavaScript, TypeScript, Python을 포함한 다양한 프로그래밍 언어에 대한 사전 구축된 런타임 모드입니다.

### 이점

- **향상된 에이전트 정확성**: 에이전트가 복잡한 계산과 데이터 처리를 수행할 수 있도록 합니다.
- **엔터프라이즈급 보안**: 격리된 환경으로 엄격한 보안 요구 사항을 충족합니다.
- **효율적인 데이터 처리**: Amazon S3의 파일을 참조하여 기가바이트 규모의 데이터를 처리할 수 있습니다.

## Amazon Bedrock AgentCore Browser Tool

### 주요 기능

1. **모델 독립적 유연성**: Anthropic의 Claude, OpenAI의 모델, Amazon의 Nova 모델을 포함한 다양한 AI 모델의 다양한 명령 구문을 지원합니다.

2. **엔터프라이즈급 보안**: VM 수준 격리, VPC 연결 및 엔터프라이즈 SSO 시스템과의 통합을 제공합니다.

3. **포괄적인 감사 기능**: 모든 브라우저 명령의 CloudTrail 로깅과 세션 기록 기능을 포함합니다.

### 이점

- **엔드투엔드 자동화**: AI 에이전트가 이전에 수동 개입이 필요했던 복잡한 웹 워크플로를 자동화할 수 있도록 합니다.
- **향상된 보안**: 광범위한 보안 기능과 감사 기능으로 엔터프라이즈 요구 사항을 충족합니다.
- **실시간 모니터링**: 즉시 개입을 위한 Live View와 디버깅 및 감사를 위한 Session Replay를 제공합니다.

## 사용 사례

- 안전한 환경에서의 복잡한 데이터 분석 및 시각화
- 양식 작성, 데이터 추출 및 다단계 프로세스를 위한 자동화된 웹 상호 작용
- 대규모 데이터 처리 및 모니터링
- 엔터프라이즈 환경에서 AI 에이전트를 위한 안전한 코드 실행

## 튜토리얼 개요

1. [Amazon Bedrock AgentCore Code Interpreter](01-Agent-Core-code-interpreter)
2. [Amazon Bedrock AgentCore Browser Tool](02-Agent-Core-browser-tool)
