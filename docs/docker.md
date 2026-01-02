# Docker 가이드

이 프로젝트는 Docker를 사용하여 일관된 개발 및 배포 환경을 제공합니다. 애플리케이션은 Nginx를 웹 서버로 사용하여 정적 파일을 서빙하도록 구성되어 있습니다.

## 🐳 Docker 설정 분석

### Dockerfile 구조

**파일**: `Dockerfile`

멀티 스테이지 빌드(Multi-stage build) 전략을 사용하여 이미지 크기를 최적화했습니다.

1. **Builder Stage (`node:20-alpine`)**
   - 소스 코드를 복사하고 의존성을 설치합니다 (`npm ci`).
   - 애플리케이션을 빌드하여 `dist/` 폴더에 정적 파일을 생성합니다 (`npm run build`).
   - 레이어 캐싱을 활용하기 위해 `package.json`을 먼저 복사합니다.

2. **Production Stage (`nginx:alpine`)**
   - 경량화된 Nginx 이미지를 기반으로 합니다.
   - Builder 단계에서 생성된 `dist/` 폴더를 Nginx의 html 경로로 복사합니다.
   - 커스텀 `nginx.conf`를 적용합니다.
   - 80번 포트를 노출합니다.

### Nginx 설정

**파일**: `nginx.conf`

- **SPA 라우팅**: 모든 요청을 `index.html`로 리다이렉트하여 React Router가 클라이언트 사이드 라우팅을 처리할 수 있게 합니다 (`try_files $uri $uri/ /index.html`).
- **캐싱 전략**: 이미지, 폰트 등 정적 자산에 대해 긴 만료 시간(6개월)을 설정하여 성능을 최적화합니다.
- **에러 페이지**: 50x 에러 발생 시 사용자에게 보여줄 페이지를 설정합니다.

---

## 🛠️ Docker Compose 사용법

**파일**: `docker-compose.yml`

로컬 환경에서 컨테이너를 쉽게 실행하고 관리하기 위한 설정입니다.

### 서비스 실행

```bash
# 백그라운드 모드로 실행
docker-compose up -d

# 이미지를 다시 빌드하고 실행
docker-compose up -d --build

# 실행 중인 컨테이너 중지
docker-compose down
```

### 환경 변수 설정

`.env` 파일을 통해 컨테이너 설정을 조정할 수 있습니다:

```bash
PORT=3000           # 호스트 머신 포트
NODE_ENV=production # 노드 환경
IMAGE_TAG=latest    # 사용할 이미지 태그
```

### 로그 확인

```bash
# 실시간 로그 확인
docker-compose logs -f

# 특정 서비스 로그 확인
docker-compose logs -f frontend
```

---

## 📦 Docker 명령어 가이드

Docker Compose를 사용하지 않고 직접 Docker 명령어를 사용할 경우의 예시입니다.

### 이미지 빌드

```bash
docker build -t react-template:latest .
```

### 컨테이너 실행

```bash
# 호스트의 3000번 포트를 컨테이너의 80번 포트에 매핑
docker run -p 3000:80 react-template:latest
```

### 컨테이너 접속 (디버깅)

```bash
# 실행 중인 컨테이너 ID 확인
docker ps

# 쉘 접속
docker exec -it <container-id> sh
```
