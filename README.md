# github-actions-lab

깃허브액션 연구소

## 프로젝트 소개

GitHub Actions를 활용한 AI 기반 자동 코드 리뷰 시스템을 실험하고 연구하는 프로젝트입니다. Ollama AI 모델을 사용하여 Pull Request와 코드 변경사항을 자동으로 분석하고 리뷰 코멘트를 생성합니다.

## 주요 기능

### 1. 자동 코드 리뷰 (Pull Request)

- Pull Request가 열리거나 업데이트될 때 자동 실행
- AI가 코드 변경사항을 분석하여 리뷰 코멘트 생성
- PR에 자동으로 인라인 코멘트 작성

### 2. Push 이벤트 코드 리뷰

- `feature/gemini` 브랜치의 `backend/**` 경로에 변경사항이 푸시될 때 실행
- 마크다운 형식의 상세한 리뷰 피드백 생성
- 리뷰 결과를 워크플로우 아티팩트로 저장

## 워크플로우 구조

워크플로우는 `.github/workflows/code-review.yml`에 정의되어 있으며 다음 단계로 구성됩니다:

1. **코드 체크아웃**: 전체 git 히스토리 가져오기
2. **Diff 생성**: 변경사항 추출 (PR 또는 Push에 따라 다름)
3. **AI 코드 리뷰**: Ollama API를 호출하여 리뷰 생성
4. **결과 처리**: PR 코멘트 작성 또는 아티팩트 업로드

## 기술 스택

- **CI/CD**: GitHub Actions
- **AI 모델**: Ollama
- **언어**: Python, Shell scripting
- **도구**: git, curl, jq

## 설정 방법

### 필요한 Secrets

워크플로우를 사용하려면 다음 GitHub Secrets를 설정해야 합니다:

- `REVIEW_API_URL`: Ollama API 엔드포인트 URL
- `REVIEW_MODEL_NAME`: 사용할 Ollama 모델 이름 (예: `llama2`, `codellama`)

### Secrets 설정 방법

1. GitHub 레포지토리의 Settings > Secrets and variables > Actions로 이동
2. "New repository secret" 클릭
3. 위의 필요한 secrets를 추가

## 워크플로우 트리거

### Pull Request 리뷰
```yaml
on:
  pull_request:
    types: [opened, synchronize]
```

### Push 이벤트 리뷰
```yaml
on:
  push:
    branches:
      - feature/gemini
    paths:
      - 'backend/**'
```

## 권한

워크플로우는 다음 권한이 필요합니다:

- `contents: read` - 레포지토리 내용 읽기
- `pull-requests: write` - PR 리뷰 코멘트 작성

## 프로젝트 파일

- `main.py`: Python 예제 코드
- `.github/workflows/code-review.yml`: 자동 코드 리뷰 워크플로우
- `main.txt`: 브랜치 참조 파일

## 사용 예시

1. 새로운 브랜치를 만들고 코드를 수정합니다
2. Pull Request를 생성합니다
3. 워크플로우가 자동으로 실행되어 코드를 분석합니다
4. AI가 생성한 리뷰 코멘트가 PR에 자동으로 달립니다

## 라이선스

이 프로젝트는 실험 및 연구 목적으로 만들어졌습니다.
