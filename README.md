# React Template 🚀

> Production-ready React + Vite template with TypeScript support, Tailwind CSS, ESLint, Prettier, Husky, Docker, and CI/CD pipelines.

[![CI](https://github.com/buenhyden/React-template/workflows/CI/badge.svg)](https://github.com/buenhyden/React-template/actions)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

---

## 📑 Table of Contents

- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Quick Start](#-quick-start)
- [Project Structure](#-project-structure)
- [Available Scripts](#-available-scripts)
- [Development](#-development)
- [Git Workflow](#-git-workflow)
- [Docker](#-docker)
- [CI/CD](#-cicd)
- [Environment Variables](#-environment-variables)

---

## ✨ Features

- ⚡️ **Vite 7** - Lightning-fast HMR and build tool
- ⚛️ **React 19** - Latest React with modern hooks
- 🎨 **Tailwind CSS** - Utility-first CSS framework
- 📝 **ESLint + Prettier** - Code quality and formatting
- 🐶 **Husky** - Git hooks for automated checks
- 🔄 **Git Flow** - Standard branching strategy
- 🐳 **Docker** - Ready for containerization
- 🚀 **GitHub Actions** - CI/CD pipelines
- 🎯 **State Management** - Zustand for simple state management
- 🎭 **Icons** - Lucide React icons library

---

## 🛠 Tech Stack

### Core

- **React** `^19.2.0` - UI framework
- **Vite** `^7.2.4` - Build tool with SWC
- **JavaScript** - Primary language (TypeScript types included)

### Styling

- **Tailwind CSS** `^3.4.17` - Utility-first CSS
- **PostCSS** `^8.5.6` - CSS processing
- **Autoprefixer** `^10.4.22` - Vendor prefixes

### State & Utilities

- **Zustand** `^5.0.8` - State management
- **clsx** `^2.1.1` - Conditional class names
- **tailwind-merge** `^3.4.0` - Merge Tailwind classes
- **lucide-react** `^0.554.0` - Icon library

### Code Quality

- **ESLint** `^9.39.1` - Linting
- **Prettier** `^3.6.2` - Code formatting
- **Husky** `^9.0.11` - Git hooks
- **lint-staged** `^15.2.10` - Run linters on staged files

---

## 🚀 Quick Start

### Prerequisites

- **Node.js** >= 20.x
- **npm** >= 10.x

### Installation

1. **Use this template** on GitHub or clone the repository:

   ```bash
   git clone https://github.com/buenhyden/React-template.git
   cd React-template
   ```

2. **Install dependencies**:

   ```bash
   npm install
   ```

3. **Start development server**:

   ```bash
   npm run dev
   ```

4. **Open your browser**: http://localhost:5173

---

## 📂 Project Structure

```
.
├── .github/
│   └── workflows/          # GitHub Actions workflows
│       ├── ci.yml          # Continuous Integration
│       ├── cd.yml          # Continuous Deployment
│       └── release.yml     # Release automation
├── .husky/                 # Git hooks
│   └── pre-commit          # Pre-commit hook (lint-staged)
├── public/                 # Static assets
│   └── vite.svg
├── scripts/                # Utility scripts
│   └── check-file-size.js  # File size validation
├── src/
│   ├── assets/             # Images, fonts, etc.
│   ├── components/         # React components
│   │   └── HelloWorld.jsx
│   ├── hooks/              # Custom React hooks
│   │   └── useCounter.js
│   ├── App.jsx             # Main App component
│   ├── App.css             # App styles
│   ├── index.css           # Global styles
│   └── main.jsx            # Application entry point
├── .dockerignore
├── .env.example            # Environment variables template
├── .gitignore
├── .gitmessage             # Git commit message template
├── .prettierrc             # Prettier configuration
├── docker-compose.yml      # Docker Compose setup
├── Dockerfile              # Docker image definition
├── eslint.config.js        # ESLint configuration
├── index.html              # HTML entry point
├── nginx.conf              # Nginx configuration for production
├── package.json            # Dependencies and scripts
├── postcss.config.js       # PostCSS configuration
├── tailwind.config.js      # Tailwind CSS configuration
└── vite.config.js          # Vite configuration
```

---

## 📜 Available Scripts

### Development

```bash
npm run dev          # Start development server (localhost:5173)
npm run build        # Build for production
npm run preview      # Preview production build locally
```

### Code Quality

```bash
npm run lint         # Run ESLint
npm run lint:fix     # Fix ESLint errors automatically
npm run format       # Format code with Prettier
```

### Validation

```bash
npm run check:merge-conflicts  # Check for merge conflict markers
npm run check:file-size        # Validate file sizes (max 1MB)
```

---

## 💻 Development

### Code Style

This project uses **ESLint** and **Prettier** for consistent code style:

- **ESLint**: Enforces code quality rules
- **Prettier**: Handles code formatting
- **EditorConfig**: Ensures consistent editor settings

Configuration files:

- `.prettierrc` - Prettier rules
- `eslint.config.js` - ESLint rules (flat config)

### Git Hooks (Husky)

Automated checks run on every commit:

1. **Merge conflict detection** - Prevents commits with conflict markers
2. **ESLint** - Auto-fixes JavaScript/JSX files
3. **Prettier** - Auto-formats all supported files
4. **File size check** - Warns about large files (>1MB)

**Hook configuration**: `.husky/pre-commit`

### lint-staged Configuration

Staged files are automatically processed:

```json
{
  "*.{js,jsx}": ["eslint --fix", "prettier --write"],
  "*.{json,css,md,yml,yaml}": ["prettier --write"],
  "*": ["npm run check:merge-conflicts"]
}
```

---

## 🌿 Git Workflow

This project follows **Git Flow** branching strategy.

### Branch Structure

| Branch      | Purpose               | Base Branch |
| ----------- | --------------------- | ----------- |
| `main`      | Production-ready code | -           |
| `develop`   | Integration branch    | `main`      |
| `feature/*` | New features          | `develop`   |
| `release/*` | Release preparation   | `develop`   |
| `hotfix/*`  | Production fixes      | `main`      |

### Workflow Commands

#### Initialize Git Flow

```bash
git flow init
# Accept defaults: main, develop, feature/, release/, hotfix/, support/
```

#### Feature Development

```bash
# Start new feature
git flow feature start feature-name

# Work on feature...
git add .
git commit -m "feat: add new feature"

# Finish feature (merges to develop)
git flow feature finish feature-name
```

#### Release Process

```bash
# Start release
git flow release start 1.0.0

# Prepare release (update version, changelog, etc.)
git commit -m "chore: prepare release 1.0.0"

# Finish release (merges to main and develop, creates tag)
git flow release finish 1.0.0

# Push tags
git push origin --tags
```

#### Hotfix

```bash
# Start hotfix
git flow hotfix start hotfix-name

# Fix the issue
git commit -m "fix: critical bug"

# Finish hotfix (merges to main and develop)
git flow hotfix finish hotfix-name
```

### Commit Message Convention

We use **Conventional Commits**:

```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types**: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`

Example:

```bash
git commit -m "feat(auth): add login functionality"
```

---

## 🐳 Docker

### Build Image

```bash
docker build -t react-template:latest .
```

### Run with Docker

```bash
docker run -p 3000:80 react-template:latest
```

### Docker Compose

```bash
# Start
docker-compose up -d

# Stop
docker-compose down

# View logs
docker-compose logs -f
```

#### Environment Variables

Create `.env` file:

```bash
REGISTRY=ghcr.io
IMAGE_NAME=buenhyden/hy-home.frontend
IMAGE_TAG=latest
PORT=3000
NODE_ENV=production
```

#### Access Application

http://localhost:3000

---

## 🚀 CI/CD

### GitHub Actions Workflows

#### 1. **CI** (`.github/workflows/ci.yml`)

Runs on push to:

- `main`
- `develop`
- `feature/**`
- `release/**`
- `hotfix/**`

**Steps**:

1. Checkout code
2. Setup Node.js 20.x
3. Install dependencies
4. Run ESLint
5. Build project

#### 2. **CD** (`.github/workflows/cd.yml`)

Automated deployment pipeline.

#### 3. **Release** (`.github/workflows/release.yml`)

Automated release creation and tagging.

---

## 🔐 Environment Variables

Create `.env` file from template:

```bash
cp .env.example .env
```

Available variables:

```bash
# API Configuration
VITE_API_URL=http://localhost:3000/api

# Environment
VITE_APP_ENV=development
```

**Note**: Only variables prefixed with `VITE_` are exposed to the client.

---

## 📝 License

This project is licensed under the **MIT License**.

---

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git flow feature start amazing-feature`)
3. Commit your changes (`git commit -m 'feat: add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/buenhyden/React-template/issues)
- **Discussions**: [GitHub Discussions](https://github.com/buenhyden/React-template/discussions)

---

**Made with ❤️ by [buenhyden](https://github.com/buenhyden)**
