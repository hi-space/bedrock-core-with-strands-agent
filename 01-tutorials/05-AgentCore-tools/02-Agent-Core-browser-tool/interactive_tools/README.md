# Amazon Bedrock AgentCore SDK 도구 예제

이 폴더에는 AgentCore SDK 도구 사용을 보여주는 예제가 포함되어 있습니다:

## 브라우저 도구

* `browser_viewer.py` - 적절한 디스플레이 크기 조정 지원을 갖춘 Amazon Bedrock AgentCore Browser Live Viewer
* `run_live_viewer.py` - Bedrock AgentCore Browser Live Viewer를 실행하는 독립 실행형 스크립트

## Code Interpreter 도구

* `dynamic_research_agent_langgraph.py` - 동적 코드 생성을 갖춘 LangGraph 기반 연구 에이전트

## 전제 조건

### Python 종속성
```bash
pip install -r requirements.txt
```

필요한 패키지: fastapi, uvicorn, rich, boto3, bedrock-agentcore

### AWS 자격 증명 (S3 저장용)
S3 기록 저장을 위해 AWS 자격 증명이 구성되어 있는지 확인하세요:
```bash
aws configure
```

## 예제 실행

### Browser Live Viewer
`02-Agent-Core-browser-tool` 디렉토리에서:
```bash
python -m interactive_tools.run_live_viewer
```

### 동적 연구 에이전트
`02-Agent-Core-browser-tool` 디렉토리에서:
```bash
python -m interactive_tools.dynamic_research_agent_langgraph
```

### Bedrock 모델 액세스
동적 연구 에이전트 예제는 Amazon Bedrock의 Claude 모델을 사용합니다:
- AWS 계정에서 Anthropic Claude 모델에 대한 액세스가 필요합니다
- 기본 모델은 `anthropic.claude-3-5-sonnet-20240620-v1:0`입니다
- `dynamic_research_agent_langgraph.py`에서 이 줄을 수정하여 모델을 변경할 수 있습니다:
  ```python
  # DynamicResearchAgent.__init__()의 38번째 줄
  self.llm = ChatBedrockConverse(
      model="anthropic.claude-3-5-sonnet-20240620-v1:0", # <- 선호하는 모델로 변경
      region_name=region
  )
  ```
- [Amazon Bedrock 콘솔](https://console.aws.amazon.com/bedrock/home#/modelaccess)에서 모델 액세스를 요청하세요

### 세션 재생
`02-Agent-Core-browser-tool/interactive_tools` 디렉토리에서:
```bash
python -m live_view_sessionreplay.browser_interactive_session
```

## Browser Live Viewer

Amazon DCV 기술을 사용한 실시간 브라우저 보기 기능입니다.

### 기능

**디스플레이 크기 제어**
- 1280×720 (HD)
- 1600×900 (HD+) - 기본값
- 1920×1080 (Full HD)
- 2560×1440 (2K)

**세션 제어**
- 제어 가져오기: 자동화를 비활성화하고 수동으로 상호 작용
- 제어 해제: 자동화로 제어 반환

### 구성
- 사용자 정의 포트: `BrowserViewerServer(browser_client, port=8080)`

## 브라우저 세션 기록 및 재생

디버깅, 테스트 및 데모 목적으로 브라우저 세션을 기록하고 재생합니다.

### 중요한 제한 사항
이 도구는 비디오 스트림이 아닌 rrweb을 사용하여 DOM 이벤트를 기록합니다:
- 실제 브라우저 콘텐츠(DCV 캔버스)가 검은 상자로 나타날 수 있습니다
- 픽셀 완벽한 비디오 기록을 위해서는 화면 기록 소프트웨어를 사용하세요

## 문제 해결

### DCV SDK를 찾을 수 없음
DCV SDK 파일이 `interactive_tools/static/dcvjs/`에 배치되어 있는지 확인하세요

### 브라우저 세션이 보이지 않음
- 브라우저 콘솔(F12)에서 오류 확인
- AWS 자격 증명에 적절한 권한이 있는지 확인

### 재생 중 기록을 찾을 수 없음
- 기록이 저장될 때 표시된 정확한 경로 확인
- S3 기록의 경우 전체 S3 URL 사용
- `aws s3 ls` 또는 `ls` 명령을 사용하여 파일이 존재하는지 확인

### S3 액세스 오류
- AWS 자격 증명이 구성되어 있는지 확인
- S3 작업에 대한 IAM 권한 확인
- 버킷 이름이 전역적으로 고유한지 확인

## 성능 고려 사항
- 기록은 브라우저 성능에 오버헤드를 추가합니다
- 파일 크기는 일반적으로 분당 1-10MB입니다
- S3 업로드는 기록이 중지된 후에 발생합니다
- 재생은 전체 파일을 먼저 다운로드해야 합니다

## 아키텍처 참고 사항
- Live viewer는 FastAPI를 사용하여 사전 서명된 DCV URL을 제공합니다
- 기록은 rrweb 라이브러리를 통해 DOM 이벤트를 캡처합니다
- 재생은 재생을 위해 rrweb-player를 사용합니다
- 모든 구성 요소는 동일한 BrowserClient 인스턴스를 공유합니다
- 모듈식 설계로 각 구성 요소의 독립적인 사용이 가능합니다