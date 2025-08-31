# Amazon CloudWatch의 AgentCore 관찰 가능성

이 저장소는 Amazon CloudWatch와 OpenTelemetry를 사용하여 에이전트에 대한 AgentCore 관찰 가능성을 구현하는 방법을 보여줍니다. Amazon Bedrock AgentCore Runtime 호스팅 에이전트와 인기 있는 오픈 소스 에이전트 프레임워크 모두에 대한 예제를 제공합니다.

## 프로젝트 구조

```
06-AgentCore-observability/
├── 01-Agentcore-runtime-hosted/
│   ├── images/
│   ├── .env.example
│   ├── README.md
│   ├── requirements.txt
│   └── runtime_with_strands_and_bedrock_models.ipynb
├── 02-Agent-not-hosted-on-runtime/
│   ├── CrewAI/
│   │   ├── .env.example
│   │   ├── CrewAI_Observability.ipynb
│   │   └── requirements.txt
│   ├── Langgraph/
│   │   ├── .env.example
│   │   ├── Langgraph_Observability.ipynb
│   │   └── requirements.txt
│   ├── Strands/
│   │   ├── .env.example
│   │   ├── requirements.txt
│   │   └── Strands_Observability.ipynb
│   └── README.md
├── 03-advanced-concepts/
│   └── 01-custom-span-creation/
│       ├── .env.example
│       ├── Custom_Span_Creation.ipynb
│       └── requirements.txt
├── README.md
└── utils.py
```

## 개요

이 저장소는 개발자가 GenAI 애플리케이션에 대한 관찰 가능성을 구현하는 데 도움이 되는 예제와 도구를 제공합니다. AgentCore 관찰 가능성은 개발자가 통합 운영 대시보드를 통해 에이전트 성능을 추적, 디버그 및 모니터링하는 데 도움이 됩니다. OpenTelemetry 호환 텔레메트리 지원과 에이전트 워크플로의 각 단계에 대한 상세한 시각화를 통해 Amazon CloudWatch GenAI 관찰 가능성은 개발자가 에이전트 동작에 대한 가시성을 쉽게 확보하고 대규모로 품질 표준을 유지할 수 있도록 합니다.

## 내용

### 1. Bedrock AgentCore Runtime 호스팅 (01-Agentcore-runtime-hosted)

Amazon OpenTelemetry Python Instrumentation과 Amazon CloudWatch를 사용하여 Amazon Bedrock AgentCore Runtime에 호스팅된 Strands Agent의 관찰 가능성을 보여주는 예제입니다.

### 2. 오픈 소스 에이전트 프레임워크 (02-Agent-not-hosted-on-runtime)

Amazon Bedrock AgentCore Runtime에 호스팅되지 않은 인기 있는 오픈 소스 에이전트 프레임워크의 관찰 가능성을 보여주는 예제:

- **CrewAI**: 작업을 수행하기 위해 역할을 맡아 함께 작업하는 자율 AI 에이전트 생성
- **LangGraph**: 복잡한 추론 시스템을 위한 상태 저장, 다중 액터 애플리케이션으로 LangChain 확장
- **Strands Agents**: 모델 기반 에이전트 개발을 사용하여 복잡한 워크플로를 가진 LLM 애플리케이션 구축

### 3. 고급 개념 (03-advanced-concepts)

고급 관찰 가능성 패턴 및 기법:

- **사용자 정의 스팬 생성**: 에이전트 워크플로 내의 특정 작업에 대한 상세한 추적 및 모니터링을 위해 사용자 정의 스팬을 생성하는 방법 학습

## 시작하기

1. 탐색하려는 프레임워크의 디렉토리로 이동
2. 요구 사항 설치
3. AWS 자격 증명 구성
4. `.env.example` 파일을 `.env`로 복사하고 변수 업데이트
5. Jupyter 노트북 열기 및 실행

## 전제 조건

- 적절한 권한이 있는 AWS 계정
- Python 3.10+
- Jupyter 노트북 환경
- 자격 증명으로 구성된 AWS CLI
- Transaction Search 활성화

## 정리

불필요한 요금을 피하기 위해 예제를 완료한 후 Amazon CloudWatch에서 생성된 로그 그룹 및 관련 리소스를 삭제하세요.

## 라이선스

이 프로젝트는 저장소에 명시된 조건에 따라 라이선스가 부여됩니다.