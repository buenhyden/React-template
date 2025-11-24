# React Template

This is a template for React applications using Vite and JavaScript.

## Features

-   **React** + **Vite**
-   **JavaScript**
-   **ESLint** + **Prettier** for code formatting and linting
-   **GitHub Actions** for CI (Lint & Build)
-   **Git Flow** ready

## Getting Started

### Installation

1.  Clone the repository:
    ```bash
    git clone <repository-url>
    ```
2.  Install dependencies:
    ```bash
    npm install
    ```

### Scripts

-   `npm run dev`: Start development server
-   `npm run build`: Build for production
-   `npm run lint`: Run ESLint
-   `npm run preview`: Preview production build

## Git Flow

This project uses [Git Flow](https://nvie.com/posts/a-successful-git-branching-model/) for branching strategy.

### Branches

-   `main`: Production-ready code.
-   `develop`: Integration branch for features.
-   `feature/*`: New features (branch off `develop`).
-   `release/*`: Release preparation (branch off `develop`).
-   `hotfix/*`: Quick fixes for production (branch off `main`).

### Workflow

1.  **Initialize Git Flow** (if not already done):
    ```bash
    git flow init
    ```
    Accept default branch names (`main`, `develop`, etc.).

2.  **Start a Feature**:
    ```bash
    git flow feature start my-feature
    ```

3.  **Finish a Feature**:
    ```bash
    git flow feature finish my-feature
    ```

4.  **Start a Release**:
    ```bash
    git flow release start 1.0.0
    ```

5.  **Finish a Release**:
    ```bash
    git flow release finish 1.0.0
    ```
    Don't forget to push tags: `git push origin --tags`

6.  **Hotfix**:
    ```bash
    git flow hotfix start hotfix-name
    git flow hotfix finish hotfix-name
    ```
