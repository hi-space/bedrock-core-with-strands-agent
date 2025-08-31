# 📚 Amazon Bedrock AgentCore 튜토리얼

Amazon Bedrock AgentCore 샘플 저장소의 튜토리얼 섹션에 오신 것을 환영합니다!

이 폴더에는 실습 예제를 통해 Amazon Bedrock AgentCore의 기본 기능을 학습할 수 있도록 설계된 대화형 노트북 기반 튜토리얼이 포함되어 있습니다.

튜토리얼은 Amazon Bedrock AgentCore 구성 요소별로 구성되어 있습니다:

* **Runtime**: Amazon Bedrock AgentCore Runtime은 프레임워크, 프로토콜 또는 모델 선택에 관계없이 조직이 AI 에이전트와 도구를 배포하고 확장할 수 있도록 지원하는 안전하고 서버리스 런타임 기능으로, 빠른 프로토타이핑, 원활한 확장 및 시장 출시 시간 단축을 가능하게 합니다
* **Gateway**: AI 에이전트는 데이터베이스 검색부터 메시지 전송까지 실제 작업을 수행하기 위한 도구가 필요합니다. Amazon Bedrock AgentCore Gateway는 API, Lambda 함수 및 기존 서비스를 MCP 호환 도구로 자동 변환하여 개발자가 통합을 관리하지 않고도 이러한 필수 기능을 에이전트에 빠르게 제공할 수 있도록 합니다.
* **Memory**: Amazon Bedrock AgentCore Memory는 개발자가 완전 관리형 메모리 인프라와 필요에 따라 메모리를 사용자 정의할 수 있는 기능을 통해 풍부하고 개인화된 에이전트 경험을 쉽게 구축할 수 있도록 합니다.
* **Identity**: Amazon Bedrock AgentCore Identity는 Okta, Entra, Amazon Cognito와 같은 표준 ID 공급자를 지원하면서 AWS 서비스와 Slack, Zoom과 같은 타사 애플리케이션 전반에 걸쳐 원활한 에이전트 ID 및 액세스 관리를 제공합니다.
* **Tools**: Amazon Bedrock AgentCore는 에이전트 AI 애플리케이션 개발을 단순화하는 두 가지 내장 도구를 제공합니다: Amazon Bedrock AgentCore **Code Interpreter** 도구는 AI 에이전트가 안전하게 코드를 작성하고 실행할 수 있도록 하여 정확성을 향상시키고 복잡한 엔드투엔드 작업을 해결하는 능력을 확장합니다. Amazon Bedrock AgentCore **Browser Tool**은 AI 에이전트가 완전 관리형 보안 샌드박스 환경에서 낮은 지연 시간으로 인간과 같은 정밀도로 웹사이트를 탐색하고, 다단계 양식을 완성하며, 복잡한 웹 기반 작업을 수행할 수 있도록 하는 엔터프라이즈급 기능입니다
* **Observability**: 관찰 가능성은 개발자가 통합 운영 대시보드를 통해 에이전트 성능을 추적, 디버그 및 모니터링하는 데 도움이 됩니다. OpenTelemetry 호환 텔레메트리 지원과 에이전트 워크플로의 각 단계에 대한 상세한 시각화를 통해 Amazon Bedrock AgentCore Observability는 개발자가 에이전트 동작에 대한 가시성을 쉽게 확보하고 대규모로 품질 표준을 유지할 수 있도록 합니다.

또한 실제 시나리오에서 이러한 구성 요소를 결합하는 방법을 보여주는 **엔드투엔드** 예제를 제공합니다.

## Amazon Bedrock AgentCore

Amazon Bedrock AgentCore 서비스는 독립적으로 사용하거나 결합하여 프로덕션 준비 에이전트를 만들 수 있습니다. 이들은 모든 에이전트 프레임워크(Strands Agents, LangChain, LangGraph 또는 CrewAI 등)와 Amazon Bedrock에서 사용 가능한 모든 모델 또는 그렇지 않은 모델과 함께 작동합니다.

![Amazon Bedrock AgentCore 개요](images/agentcore_overview.png)

이 튜토리얼에서는 각 서비스를 개별적으로 그리고 결합하여 사용하는 방법을 학습합니다.

## 🎯 이 튜토리얼의 대상

이 튜토리얼은 다음과 같은 분들에게 적합합니다:

 - Amazon Bedrock AgentCore 시작하기
 - 고급 애플리케이션을 구축하기 전에 핵심 개념 이해하기
 - Amazon Bedrock AgentCore를 사용한 AI 에이전트 개발의 견고한 기초 다지기
