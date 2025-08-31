# Amazon Bedrock AgentCore Memory

## 개요

메모리는 지능의 중요한 구성 요소입니다. 대규모 언어 모델(LLM)은 인상적인 기능을 가지고 있지만 대화 간에 지속적인 메모리가 부족합니다. Amazon Bedrock AgentCore Memory는 AI 에이전트가 시간이 지남에 따라 컨텍스트를 유지하고 중요한 사실을 기억하며 일관되고 개인화된 경험을 제공할 수 있도록 하는 관리형 서비스를 제공하여 이러한 한계를 해결합니다.

## 주요 기능

AgentCore Memory는 다음을 제공합니다:

- **핵심 인프라**: 내장 암호화 및 관찰 가능성을 갖춘 서버리스 설정
- **이벤트 저장**: 분기 지원을 통한 원시 이벤트 저장(대화 기록/체크포인팅)
- **전략 관리**: 구성 가능한 추출 전략(SEMANTIC, SUMMARY, USER_PREFERENCES, CUSTOM)
- **메모리 레코드 추출**: 구성된 전략을 기반으로 한 사실, 선호도 및 요약의 자동 추출
- **의미 검색**: 자연어 쿼리를 사용한 관련 메모리의 벡터 기반 검색

## AgentCore Memory 작동 방식

![고수준 워크플로](./images/high_level_memory.png)

AgentCore Memory는 두 가지 수준에서 작동합니다:

### 단기 메모리

단일 상호 작용 또는 밀접하게 관련된 세션 내에서 연속성을 제공하는 즉각적인 대화 컨텍스트 및 세션 기반 정보입니다.

### 장기 메모리

여러 대화에 걸쳐 추출되고 저장된 지속적인 정보로, 시간이 지남에 따라 개인화된 경험을 가능하게 하는 사실, 선호도 및 요약을 포함합니다.

## 메모리 아키텍처

1. **대화 저장**: 완전한 대화가 즉시 액세스를 위해 원시 형태로 저장됩니다
2. **전략 처리**: 구성된 전략이 백그라운드에서 대화를 자동으로 분석합니다
3. **정보 추출**: 전략 유형에 따라 중요한 데이터가 추출됩니다(일반적으로 ~1분 소요)
4. **체계적 저장**: 추출된 정보가 효율적인 검색을 위해 구조화된 네임스페이스에 저장됩니다
5. **의미 검색**: 자연어 쿼리가 벡터 유사성을 사용하여 관련 메모리를 검색할 수 있습니다

## 메모리 전략 유형

AgentCore Memory는 네 가지 전략 유형을 지원합니다:

- **의미 메모리**: 유사성 검색을 위해 벡터 임베딩을 사용하여 사실 정보를 저장합니다
- **요약 메모리**: 컨텍스트 보존을 위해 대화 요약을 생성하고 유지합니다
- **사용자 선호도 메모리**: 사용자별 선호도와 설정을 추적합니다
- **사용자 정의 메모리**: 추출 및 통합 로직의 사용자 정의를 허용합니다

## 시작하기

체계적으로 구성된 튜토리얼을 통해 메모리 기능을 탐색하세요:

- **[단기 메모리](./01-short-term-memory/)**: 세션 기반 메모리와 즉각적인 컨텍스트 관리에 대해 학습합니다
- **[장기 메모리](./02-long-term-memory/)**: 지속적인 메모리 전략과 대화 간 연속성을 이해합니다

## 샘플 노트북 개요

| 메모리 유형 | 프레임워크           | 사용 사례           | 노트북                                                                                                                           |
| ----------- | ------------------- | ------------------ | ---------------------------------------------------------------------------------------------------------------------------------- |
| 단기  | Strands Agent       | 개인 에이전트     | [personal-agent.ipynb](./01-short-term-memory/01-single-agent/with-strands-agent/personal-agent.ipynb)                             |
| 단기  | LangGraph           | 피트니스 코치      | [personal-fitness-coach.ipynb](./01-short-term-memory/01-single-agent/with-langgraph-agent/personal-fitness-coach.ipynb)           |
| 단기  | Strands Agent       | 여행 계획    | [travel-planning-agent.ipynb](./01-short-term-memory/02-multi-agent/with-strands-agent/travel-planning-agent.ipynb)                |
| 장기   | Strands Hooks       | 고객 지원   | [customer-support.ipynb](./02-long-term-memory/01-single-agent/using-strands-agent-hooks/customer-support/customer-support.ipynb)  |
| 장기   | Strands Hooks       | 수학 도우미     | [math-assistant.ipynb](./02-long-term-memory/01-single-agent/using-strands-agent-hooks/simple-math-assistant/math-assistant.ipynb) |
| 장기   | Strands Tool        | 요리 도우미 | [culinary-assistant.ipynb](./02-long-term-memory/01-single-agent/using-strands-agent-memory-tool/culinary-assistant.ipynb)         |
| 장기   | Strands Multi-Agent | 여행 예약     | [travel-booking-assistant.ipynb](./02-long-term-memory/02-multi-agent/with-strands-agent/travel-booking-assistant.ipynb)           |

## 전제 조건

- Python 3.10 이상
- Amazon Bedrock 액세스가 있는 AWS 계정
- Jupyter Notebook 환경
- 필요한 Python 패키지(개별 샘플 requirements.txt 파일 참조)
