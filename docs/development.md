# 개발 환경 가이드

프로젝트 개발을 시작하기 위한 환경 설정 및 코드 품질 관리 도구에 대한 설명입니다.

## 💻 필수 요구 사항

- **Node.js**: v20.x 이상
- **npm**: v10.x 이상
- **Git**: 최신 버전

## 🚀 시작하기

1. **저장소 클론**

   ```bash
   git clone https://github.com/buenhyden/React-template.git
   cd React-template
   ```

2. **의존성 설치**

   ```bash
   npm install
   ```

3. **개발 서버 실행**
   ```bash
   npm run dev
   ```
   브라우저에서 `http://localhost:5173`으로 접속하여 확인합니다.

---

## 🎨 코드 스타일 및 품질 관리

일관된 코드 스타일과 품질을 유지하기 위해 다음 도구들을 사용합니다.

### ESLint & Prettier

- **ESLint**: 코드의 잠재적인 오류와 안티 패턴을 찾아냅니다. (`eslint.config.js`)
- **Prettier**: 코드를 자동으로 포맷팅하여 스타일을 통일합니다. (`.prettierrc`)

**주요 명령어**:

```bash
npm run lint         # 코드 검사
npm run lint:fix     # 코드 검사 및 자동 수정
npm run format       # Prettier 포맷팅 실행
```

### EditorConfig

`.editorconfig` 파일을 통해 다양한 에디터에서 동일한 들여쓰기 및 공백 설정을 유지합니다. VS Code 사용 시 `EditorConfig for VS Code` 확장 프로그램을 설치하는 것을 권장합니다.

---

## 📝 커밋 템플릿 설정

이 프로젝트는 일관된 커밋 메시지 작성을 위해 커밋 템플릿을 제공합니다.

### 템플릿 설정 방법

프로젝트 루트에 있는 `.gitmessage` 파일을 Git 설정에 등록하여 사용할 수 있습니다.

```bash
git config commit.template .gitmessage
```

### 템플릿 구조

템플릿은 다음과 같은 구조로 되어 있습니다:

```
<type>: <제목>

<Body Message> (선택사항)

<Footer> (선택사항)
```

- **제목**: 50자 이내, 명확한 변경 사항 기술 (마침표 제외)
- **본문**: "어떻게"보다 "무엇을", "왜" 변경했는지 설명
- **타입**: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore` 등

---

## 🐶 Git Hooks (Husky)

Git 커밋 및 푸시 과정에서 자동으로 품질 검사를 수행하기 위해 [Husky](https://typicode.github.io/husky/)를 사용합니다.

### Pre-commit Hook

`git commit` 명령 실행 시 `.husky/pre-commit` 스크립트가 먼저 실행됩니다. 이 훅은 다음 두 가지 주요 작업을 수행합니다:

1. **머지 충돌 마커 검사**: 코드 내에 해결되지 않은 충돌 마커(`<<<<<<<`, `=======`, `>>>>>>>`)가 있는지 검사합니다. 발견 시 커밋을 중단합니다.
2. **lint-staged 실행**: 스테이징된 파일들에 대해 린트 및 포맷팅 작업을 수행합니다.

### lint-staged 설정

`package.json`에 정의된 `lint-staged` 설정에 따라, 커밋하려는 파일(staged files)에 대해서만 다음 작업들이 자동으로 수행됩니다:

- **JavaScript/React 파일** (`*.{js,jsx}`)
  - `eslint --fix`: 코드 오류를 찾고 가능한 경우 자동으로 수정합니다.
  - `prettier --write`: 코드 스타일을 포맷팅합니다.
- **설정 및 문서 파일** (`*.{json,css,md,yml,yaml}`)
  - `prettier --write`: 코드 스타일을 포맷팅합니다.

- **모든 파일** (`*`)
  - `npm run check:merge-conflicts`: 머지 충돌 마커가 있는지 다시 한 번 확인합니다.

이 과정을 통해 커밋되는 모든 코드는 항상 깨끗하고 일관된 상태를 유지하게 됩니다.

### 파일 크기 제한

`scripts/check-file-size.js` 스크립트를 통해 저장소 용량을 효율적으로 관리합니다. 실수로 대용량 바이너리 파일이 커밋되는 것을 방지합니다.

---

## 🛠 유용한 스크립트

`package.json`에 정의된 주요 스크립트입니다:

| 스크립트                | 설명                                |
| :---------------------- | :---------------------------------- |
| `dev`                   | 개발 서버 실행 (HMR 지원)           |
| `build`                 | 프로덕션용 빌드 생성 (`dist/` 폴더) |
| `preview`               | 빌드된 결과물을 로컬에서 미리보기   |
| `check:merge-conflicts` | 머지 충돌 마커 검사                 |
| `check:file-size`       | 파일 크기 검사                      |
