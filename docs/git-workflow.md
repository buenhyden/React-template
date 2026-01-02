# Git 워크플로우 전략

이 프로젝트는 **Git Flow** 브랜치 전략을 따르며, **Conventional Commits** 규칙을 준수하여 이력을 관리합니다.

## 🌿 Git Flow 브랜치 구조

| 브랜치      | 역할                       | 기반 브랜치 | 병합 대상         |
| :---------- | :------------------------- | :---------- | :---------------- |
| `main`      | 배포 가능한 프로덕션 코드  | -           | -                 |
| `develop`   | 다음 배포를 위한 개발 코드 | `main`      | `main`            |
| `feature/*` | 새로운 기능 개발           | `develop`   | `develop`         |
| `release/*` | 배포 준비 및 버전 테스팅   | `develop`   | `main`, `develop` |
| `hotfix/*`  | 프로덕션 긴급 버그 수정    | `main`      | `main`, `develop` |

---

## 🔄 작업 흐름 가이드

### 1. 기능 개발 (Feature)

새로운 기능을 개발할 때 사용합니다.

```bash
# 1. 기능 브랜치 시작
git flow feature start my-feature

# 2. 작업 및 커밋
git add .
git commit -m "feat(user): add login page"

# 3. 기능 개발 완료 (develop에 병합)
git flow feature finish my-feature
```

### 2. 릴리스 준비 (Release)

배포 버전을 준비하고 QA를 진행할 때 사용합니다.

```bash
# 1. 릴리스 브랜치 시작 (버전 지정)
git flow release start 1.0.0

# 2. 버전 정보 업데이트, changelog 작성 등
git commit -m "chore: bump version to 1.0.0"

# 3. 릴리스 완료 (main과 develop에 병합 및 태그 생성)
git flow release finish 1.0.0
git push origin --tags
```

### 3. 긴급 수정 (Hotfix)

운영 중인 서비스(`main`)에서 버그가 발생했을 때 사용합니다.

```bash
# 1. 핫픽스 브랜치 시작
git flow hotfix start login-error

# 2. 버그 수정
git commit -m "fix(auth): fix login timeout issue"

# 3. 핫픽스 완료
git flow hotfix finish login-error
```

---

## 📝 커밋 메시지 컨벤션 (Conventional Commits)

명확한 히스토리 관리를 위해 다음 형식을 따릅니다:

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Type 종류

- **feat**: 새로운 기능 추가
- **fix**: 버그 수정
- **docs**: 문서 수정
- **style**: 코드 포맷팅, 세미콜론 누락 등 (비즈니스 로직 변경 없음)
- **refactor**: 코드 리팩토링
- **test**: 테스트 코드 추가 또는 수정
- **chore**: 빌드 업무 수정, 패키지 매니저 설정 등

### 예시

```bash
feat(auth): 로그인 API 연동 기능 추가
fix(ui): 모바일 헤더 깨짐 현상 수정
docs(readme): 설치 가이드 업데이트
```

### Git Commit Template

프로젝트 루트의 `.gitmessage` 파일을 통해 커밋 템플릿을 사용할 수 있습니다. 이를 설정하려면 다음 명령어를 실행하세요:

```bash
git config commit.template .gitmessage
```
