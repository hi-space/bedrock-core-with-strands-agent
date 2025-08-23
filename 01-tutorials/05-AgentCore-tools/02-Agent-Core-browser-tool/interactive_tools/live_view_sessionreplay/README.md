# Amazon Bedrock AgentCore SDK 도구 예제

이 폴더에는 Amazon Bedrock AgentCore SDK 도구 사용을 보여주는 예제가 포함되어 있습니다:

## 브라우저 도구

* `browser_viewer_replay.py` - 적절한 디스플레이 크기 조정 지원을 갖춘 Amazon Bedrock AgentCore Browser Live Viewer
* `browser_interactive_session.py` - 라이브 보기, 기록 및 재생 기능을 갖춘 완전한 엔드투엔드 브라우저 경험
* `session_replay_viewer.py` - 기록된 브라우저 세션을 재생하는 뷰어
* `view_recordings.py` - S3에서 기록된 세션을 보는 독립 실행형 스크립트

## 전제 조건

### Python 종속성
```bash
pip install -r requirements.txt
```

필요한 패키지: fastapi, uvicorn, rich, boto3, bedrock-agentcore

### AWS 자격 증명
AWS 자격 증명이 구성되어 있는지 확인하세요:
```bash
aws configure
```

## 예제 실행

### 기록 및 재생을 포함한 완전한 브라우저 경험
`02-Agent-Core-browser-tool/interactive_tools` 디렉토리에서:
```bash
python -m live_view_sessionreplay.browser_interactive_session
```

### 기록 보기
`02-Agent-Core-browser-tool/interactive_tools` 디렉토리에서:
```bash
python -m live_view_sessionreplay.view_recordings --bucket YOUR_BUCKET --prefix YOUR_PREFIX
```

## 기록 및 재생을 포함한 완전한 브라우저 경험

라이브 브라우저 보기, S3에 자동 기록 및 통합 세션 재생을 포함하는 완전한 엔드투엔드 워크플로를 실행합니다.

### 기능
- S3에 자동 기록이 포함된 브라우저 세션 생성
- 대화형 제어(가져오기/해제)가 있는 라이브 보기
- 실시간으로 디스플레이 해상도 조정
- S3에 자동 세션 기록
- 기록을 시청하기 위한 통합 세션 재생 뷰어

### 작동 방식
1. 스크립트가 기록이 활성화된 브라우저를 생성합니다
2. 브라우저 세션이 시작되고 로컬 브라우저에 표시됩니다
3. 브라우저를 수동으로 제어하거나 자동화를 실행할 수 있습니다
4. 모든 작업이 자동으로 S3에 기록됩니다
5. 세션을 종료한 후(Ctrl+C) 기록을 보여주는 재생 뷰어가 열립니다

### 환경 변수
- `AWS_REGION` - AWS 지역 (기본값: us-west-2)
- `AGENTCORE_ROLE_ARN` - 브라우저 실행을 위한 IAM 역할 ARN (기본값: 계정 ID에서 자동 생성)
- `RECORDING_BUCKET` - 기록용 S3 버킷 (기본값: session-record-test-{ACCOUNT_ID})
- `RECORDING_PREFIX` - 기록용 S3 접두사 (기본값: replay-data)

### 필요한 IAM 권한
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:CreateBucket",
                "s3:PutObject",
                "s3:GetObject",
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::session-record-test-*",
                "arn:aws:s3:::session-record-test-*/*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": "bedrock:*",
            "Resource": "*"
        }
    ]
}
```

## 독립 실행형 세션 재생 뷰어

새 브라우저를 생성하지 않고 S3에서 직접 기록된 브라우저 세션을 보는 별도 도구입니다.

### 기능
- S3에 직접 연결하여 기록 보기
- 세션 ID를 지정하여 과거 기록 보기
- 세션 ID가 제공되지 않으면 자동으로 최신 기록 찾기

### 사용법

```bash
# 버킷의 최신 기록 보기
python -m live_view_sessionreplay.view_recordings --bucket session-record-test-123456789012 --prefix replay-data

# 특정 기록 보기
python -m live_view_sessionreplay.view_recordings --bucket session-record-test-123456789012 --prefix replay-data --session 01JZVDG02M8MXZY2N7P3PKDQ74

# 특정 AWS 프로필 사용
python -m live_view_sessionreplay.view_recordings --bucket session-record-test-123456789012 --prefix replay-data --profile my-profile
```

### 기록 찾기

S3 기록 나열:
```bash
aws s3 ls s3://session-record-test-123456789012/replay-data/ --recursive
```

## 문제 해결

### DCV SDK를 찾을 수 없음
DCV SDK 파일이 `interactive_tools/static/dcvjs/`에 배치되어 있는지 확인하세요

### 브라우저 세션이 보이지 않음
- DCV SDK가 제대로 설치되어 있는지 확인
- 브라우저 콘솔(F12)에서 오류 확인
- AWS 자격 증명에 적절한 권한이 있는지 확인

### 기록이 작동하지 않음
- S3 버킷이 존재하고 액세스 가능한지 확인
- S3 작업에 대한 IAM 권한 확인
- 실행 역할에 적절한 권한이 있는지 확인

### 세션 재생 문제
- S3에 기록이 존재하는지 확인 (AWS CLI 또는 콘솔 사용)
- 콘솔 로그에서 오류 확인
- S3 버킷 정책이 객체 읽기를 허용하는지 확인

### S3 액세스 오류
- AWS 자격 증명이 구성되어 있는지 확인
- S3 작업에 대한 IAM 권한 확인
- 버킷 이름이 전역적으로 고유한지 확인

## 아키텍처 참고 사항
- Live viewer는 FastAPI를 사용하여 사전 서명된 DCV URL을 제공합니다
- 기록은 데이터 플레인의 브라우저 서비스에서 직접 처리됩니다
- 재생은 기록된 이벤트의 재생을 위해 rrweb-player를 사용합니다
- 모든 구성 요소는 함께 또는 독립적으로 작동할 수 있습니다