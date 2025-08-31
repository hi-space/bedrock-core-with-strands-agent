# Bedrock AgentCore 에이전트를 위한 Amazon CloudWatch의 AgentCore 관찰 가능성

이 저장소는 Amazon OpenTelemetry Python Instrumentation과 Amazon CloudWatch를 사용하여 Amazon Bedrock AgentCore Runtime에 호스팅된 Strands Agent에 대한 AgentCore 관찰 가능성을 보여주는 예제를 포함합니다. 관찰 가능성은 개발자가 통합 운영 대시보드를 통해 프로덕션에서 에이전트 성능을 추적, 디버그 및 모니터링하는 데 도움이 됩니다. OpenTelemetry 호환 텔레메트리 지원과 에이전트 워크플로의 각 단계에 대한 상세한 시각화를 통해 Amazon CloudWatch GenAI 관찰 가능성은 개발자가 에이전트 동작에 대한 가시성을 쉽게 확보하고 대규모로 품질 표준을 유지할 수 있도록 합니다.

## 시작하기

프로젝트 폴더에는 다음이 포함되어 있습니다:
- Cloudwatch에서 Agentcore 런타임과 관찰 가능성을 보여주는 Jupyter 노트북
- 필요한 종속성을 나열하는 requirements.txt 파일
- 필요한 환경 변수를 보여주는 .env.example 파일

## 사용법

1. 탐색하려는 프레임워크의 디렉토리로 이동
2. 요구 사항 설치: `!pip install -r requirements.txt `
3. AWS 자격 증명 구성
3. .env.example 파일을 .env로 복사하고 변수 업데이트
4. Jupyter 노트북 열기 및 실행

### Strands Agents
[Strands](https://strandsagents.com/latest/)는 모델 기반 에이전트 개발에 중점을 두고 복잡한 워크플로를 가진 LLM 애플리케이션을 구축하기 위한 프레임워크를 제공합니다.

## 정리

관찰 가능성을 위해 Amazon CloudWatch에서 생성된 Amazon CloudWatch 로그 그룹 및 관련 리소스를 삭제하세요.
