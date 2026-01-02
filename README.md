# React Template 🚀

> Production-ready React + Vite template with TypeScript support, Tailwind CSS, ESLint, Prettier, Husky, Docker, and CI/CD pipelines.

[![CI](https://github.com/buenhyden/React-template/workflows/CI/badge.svg)](https://github.com/buenhyden/React-template/actions)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

---

## 📑 목차

- [소개](#-features)
- [기술 스택](#-tech-stack)
- [문서 (Documentation)](#-documentation)
- [빠른 시작](#-quick-start)
- [프로젝트 구조](#-project-structure)
- [기여하기](#-contributing)

---

## ✨ Features

- ⚡️ **Vite 7** - 초고속 HMR 및 빌드 도구
- ⚛️ **React 19** - 최신 React 및 모던 훅 지원
- 🎨 **Tailwind CSS** - 유틸리티 우선 CSS 프레임워크
- 📝 **ESLint + Prettier** - 코드 품질 및 포맷팅 자동화
- 🐶 **Husky** - Git Hooks를 통한 자동화된 체크
- 🔄 **Git Flow** - 표준화된 브랜치 전략
- 🐳 **Docker** - 컨테이너화 준비 완료
- 🚀 **GitHub Actions** - CI/CD 파이프라인 구축
- 🎯 **State Management** - Zustand를 이용한 간편한 상태 관리
- 🎭 **Icons** - Lucide React 아이콘 라이브러리

---

## 🛠 Tech Stack

### Core

- **React** `^19.2.0`
- **Vite** `^7.2.4`
- **JavaScript** (TypeScript 지원)

### Styling & UI

- **Tailwind CSS** `^3.4.17`
- **PostCSS**, **Autoprefixer**
- **lucide-react** (Icons), **clsx**, **tailwind-merge**

### Code Quality

- **ESLint** `^9.39.1`
- **Prettier** `^3.6.2`
- **Husky**, **lint-staged**

---

## 📚 Documentation

프로젝트에 대한 상세 문서는 `docs/` 폴더에서 확인할 수 있습니다.

| 주제          | 설명                                    | 링크                                       |
| :------------ | :-------------------------------------- | :----------------------------------------- |
| **개발 환경** | Node.js 설정, 코드 스타일, 린트 설정 등 | [👉 development.md](docs/development.md)   |
| **CI/CD**     | GitHub Actions 빌드 및 배포 파이프라인  | [👉 ci-cd.md](docs/ci-cd.md)               |
| **Docker**    | Dockerfile, Compose, Nginx 설정 가이드  | [👉 docker.md](docs/docker.md)             |
| **Git 전략**  | Git Flow 브랜치 전략 및 커밋 컨벤션     | [👉 git-workflow.md](docs/git-workflow.md) |

---

## 🚀 Quick Start

### 필수 요구 사항

- **Node.js** >= 20.x
- **npm** >= 10.x

### 설치 및 실행

```bash
# 1. 저장소 클론
git clone https://github.com/buenhyden/React-template.git
cd React-template

# 2. 의존성 설치
npm install

# 3. 개발 서버 시작
npm run dev
# Browser: http://localhost:5173
```

### 주요 스크립트

```bash
npm run build        # 프로덕션 빌드
npm run preview      # 빌드 미리보기
npm run lint         # 린트 검사
npm run format       # 코드 포맷팅
```

---

## 📂 Project Structure

```
.
├── .github/workflows/  # CI/CD (ci, cd, release)
├── .husky/             # Git Hooks
├── docs/               # 상세 프로젝트 문서 👈
├── public/             # 정적 리소스
├── scripts/            # 유틸리티 스크립트
├── src/
│   ├── assets/         # 이미지, 폰트
│   ├── components/     # 컴포넌트
│   ├── hooks/          # 커스텀 훅
│   └── main.jsx        # 진입점
├── docker-compose.yml  # Docker 설정
├── Dockerfile          # Docker 이미지 빌드 설정
└── nginx.conf          # Nginx 설정
```

---

## 🤝 Contributing

1. 저장소 Fork
2. 브랜치 생성 (`git flow feature start feature-name`)
3. 변경 사항 커밋 (`git commit -m 'feat: add amazing feature'`)
4. 브랜치 Push (`git push origin feature/feature-name`)
5. Pull Request 생성

---

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/buenhyden/React-template/issues)
- **Discussions**: [GitHub Discussions](https://github.com/buenhyden/React-template/discussions)

---

**Made with ❤️ by [buenhyden](https://github.com/buenhyden)**
