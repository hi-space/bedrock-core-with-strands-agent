# AgentCore Runtime에 호스팅되지 않은 오픈 소스 에이전트를 위한 AgentCore 관찰 가능성

이 저장소는 Amazon OpenTelemetry Python Instrumentation과 Amazon CloudWatch를 사용하여 Amazon Bedrock AgentCore Runtime에 호스팅되지 **않은** 인기 있는 AI 오픈 소스 프레임워크에 대한 AgentCore 관찰 가능성을 보여주는 예제를 포함합니다. 관찰 가능성은 개발자가 통합 운영 대시보드를 통해 프로덕션에서 에이전트 성능을 추적, 디버그 및 모니터링하는 데 도움이 됩니다. OpenTelemetry 호환 텔레메트리 지원과 에이전트 워크플로의 각 단계에 대한 상세한 시각화를 통해 Amazon CloudWatch GenAI 관찰 가능성은 개발자가 에이전트 동작에 대한 가시성을 쉽게 확보하고 대규모로 품질 표준을 유지할 수 있도록 합니다.

다음 오픈 소스 에이전트 프레임워크로 에이전트를 생성합니다:

- **CrewAI**
- **LangGraph**
- **Strands Agents**

## 프로젝트 구조

```
02-Agent-not-hosted-on-runtime/
├── CrewAI/
│   ├── .env.example
│   ├── CrewAI_Observability.ipynb
│   └── requirements.txt
├── Langgraph/
│   ├── .env.example
│   ├── Langgraph_Observability.ipynb
│   └── requirements.txt
└── Strands/
    ├── .env.example
    ├── requirements.txt
    └── Strands_Observability.ipynb
```

## 시작하기

각 프레임워크에는 다음이 포함된 자체 디렉토리가 있습니다:
- 프레임워크의 기능을 보여주는 Jupyter 노트북
- 필요한 종속성을 나열하는 requirements.txt 파일
- 필요한 환경 변수를 보여주는 .env.example 파일

## 사용법

1. 탐색하려는 프레임워크의 디렉토리로 이동
2. 요구 사항 설치: `pip install -r requirements.txt`
3. AWS 자격 증명 구성
3. .env.example 파일을 .env로 복사하고 변수 업데이트
4. Jupyter 노트북 열기 및 실행

## 프레임워크 개요

### CrewAI
[CrewAI](https://www.crewai.com/)는 작업을 수행하기 위해 역할을 맡아 함께 작업할 수 있는 자율 AI 에이전트의 생성을 가능하게 합니다.

### LangGraph
[LangGraph](https://www.langchain.com/langgraph)는 상태 저장, 다중 액터 애플리케이션으로 LangChain을 확장합니다. LLM을 사용한 복잡한 추론 시스템을 만드는 데 특히 유용합니다.

### Strands Agents
[Strands](https://strandsagents.com/latest/)는 모델 기반 에이전트 개발에 중점을 두고 복잡한 워크플로를 가진 LLM 애플리케이션을 구축하기 위한 프레임워크를 제공합니다.

## 정리

Amazon CloudWatch에서 생성된 로그 그룹 및 관련 리소스를 삭제하세요.