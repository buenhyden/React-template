# CI/CD 파이프라인

이 프로젝트는 GitHub Actions를 사용하여 지속적 통합(CI) 및 지속적 배포(CD)를 자동화하고 있습니다. 모든 워크플로우 파일은 `.github/workflows/` 디렉토리에 위치합니다.

## 🚀 워크플로우 개요

| 워크플로우  | 파일명        | 설명                          | 트리거 조건                         |
| :---------- | :------------ | :---------------------------- | :---------------------------------- |
| **CI**      | `ci.yml`      | 코드 린팅 및 빌드 테스트      | `main`, `develop` 브랜치 푸시 및 PR |
| **CD**      | `cd.yml`      | Docker 이미지 빌드 및 배포    | `main`, `develop` 브랜치 푸시       |
| **Release** | `release.yml` | 버전 태그 생성 및 릴리스 배포 | `release/**` 브랜치 푸시            |

---

## 🛠️ 1. CI (Continuous Integration)

**파일**: `.github/workflows/ci.yml`

코드 변경 사항이 발생할 때마다 자동으로 실행되어 코드 품질을 검사하고 빌드가 성공하는지 확인합니다.

### 실행 조건

- **Push**: `main`, `develop`, `feature/**`, `release/**`, `hotfix/**` 브랜치
- **Pull Request**: `main`, `develop` 브랜치 대상

### 주요 단계 (Jobs)

`build` 작업은 `ubuntu-latest` 환경에서 실행되며 다음 단계를 수행합니다:

1. **환경 설정**: Node.js 20.x 버전을 설정하고 `npm` 캐시를 활성화합니다.
2. **의존성 설치**: `npm ci`를 통해 `package-lock.json`에 명시된 의존성을 정확하게 설치합니다.
3. **린팅 (Lint)**: `npm run lint`를 실행하여 ESLint 규칙 준수 여부를 확인합니다.
4. **빌드 (Build)**: `npm run build`를 실행하여 프로덕션 빌드가 성공하는지 검증합니다.

---

## 📦 2. CD (Continuous Deployment)

**파일**: `.github/workflows/cd.yml`

검증된 코드를 Docker 이미지로 빌드하고 GitHub Container Registry (GHCR)에 푸시합니다.

### 실행 조건

- **Push**: `main`, `develop` 브랜치

### 환경 변수

- `REGISTRY`: `ghcr.io`
- `IMAGE_NAME`: GitHub 저장소 이름 (예: `buenhyden/React-template`)

### 주요 단계

1. **GitHub CR 로그인**: `GITHUB_TOKEN`을 사용하여 레지스트리에 인증합니다.
2. **메타데이터 추출**: 브랜치에 따라 이미지 태그를 자동으로 생성합니다.
   - `main` 브랜치: `latest`, `sha-<commit-hash>`
   - `develop` 브랜치: `dev`, `{{branch}}-<commit-hash>`
3. **빌드 및 푸시**: `Dockerfile`을 기반으로 이미지를 빌드하고 레지스트리에 업로드합니다.

---

## 🔖 3. Release Automation

**파일**: `.github/workflows/release.yml`

릴리스 브랜치가 푸시되면 자동으로 버전을 추출하고 릴리스 태그를 생성합니다.

### 실행 조건

- **Push**: `release/**` 패턴의 브랜치 (예: `release/1.0.0`)

### 주요 단계

1. **버전 추출**: 브랜치 이름에서 버전 번호를 파싱합니다 (예: `release/1.0.0` -> `1.0.0`).
2. **Docker 이미지 빌드**: 해당 버전으로 Docker 이미지를 빌드하고 태그를 지정하여 푸시합니다.
   - 태그 예시: `1.0.0`, `rc-1.0.0`, `1.0.0-<commit-hash>`
3. **Git 태그 생성**: `v<버전>` (예: `v1.0.0`) 형식의 Git 태그를 생성하고 원격 저장소에 푸시합니다.

## 🔑 필요한 Secrets

이 워크플로우들은 GitHub 저장소의 설정에 별도의 Secret 등록이 필요 없으며, GitHub Actions에서 자동으로 제공하는 `GITHUB_TOKEN`을 사용합니다.
