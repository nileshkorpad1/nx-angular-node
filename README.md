# ReadME - Angular Node NX Monorepo
 Nx monorepo setup with Angular frontend, Node.js/Express backend, shared libraries (constants, types, utils), Husky configuration, and Commitizen setup.

# Nx Angular Node.js Monorepo

A professional full-stack monorepo built with Nx, featuring Angular frontend, Node.js/Express.js backend, shared libraries, and enterprise-level development tools including Husky and Commitizen for commit management.

## 🏗️ Project Architecture

```
nx-angular-node/
├── apps/
│   ├── frontend/                 # Angular 18+ Application
│   │   ├── src/
│   │   │   ├── app/
│   │   │   ├── assets/
│   │   │   ├── environments/
│   │   │   └── main.ts
│   │   ├── project.json
│   │   ├── tsconfig.app.json
│   │   └── proxy.conf.json
│   ├── frontend-e2e/            # Frontend E2E Tests (Cypress)
│   │   ├── src/
│   │   ├── cypress.config.ts
│   │   └── project.json
│   ├── backend/                 # Express.js/Node.js API
│   │   ├── src/
│   │   │   ├── app/
│   │   │   ├── environments/
│   │   │   └── main.ts
│   │   ├── project.json
│   │   └── tsconfig.app.json
│   └── backend-e2e/            # Backend E2E Tests
│       ├── src/
│       ├── jest.config.ts
│       └── project.json
├── libs/
│   ├── constants/              # Shared Constants
│   │   ├── src/lib/constants.ts
│   │   └── index.ts
│   ├── types/                  # Shared TypeScript Types
│   │   ├── src/lib/types.ts
│   │   └── index.ts
│   └── utils/                  # Shared Utility Functions
│       ├── src/lib/utils.ts
│       └── index.ts
├── .husky/                     # Git Hooks Configuration
│   ├── commit-msg              # Commit message validation
│   ├── pre-commit              # Pre-commit linting & formatting
│   └── pre-push                # Branch name validation
├── .branchlintrc.json          # Branch naming rules
├── commitlint.config.js        # Commit message linting rules
├── nx.json                     # Nx workspace configuration
├── package.json                # Dependencies and scripts
├── tsconfig.base.json          # Base TypeScript configuration
└── README.md                   # This file
```

## 🚀 Quick Start

### Prerequisites

- **Node.js** 18+ and **npm** 8+
- **Git** 2.25+

### Installation

```bash
# Clone the repository
git clone <repository-url>
cd nx-angular-node

# Install dependencies
npm install

# Initialize Husky hooks
npm run prepare
```

### Development

```bash
# Start both frontend and backend in parallel
npm run dev

# Or start individually
npm run serve:frontend  # http://localhost:4200
npm run serve:backend   # http://localhost:3333
```

## 📦 Nx Command Reference

### Application Commands

#### Frontend (Angular)

```bash
nx serve frontend                    # Development server
nx build frontend                    # Production build
nx test frontend                     # Unit tests
nx test frontend --watch            # Watch mode
nx lint frontend                     # ESLint
nx lint frontend --fix              # Fix linting issues
nx e2e frontend-e2e                 # E2E tests
```

#### Backend (Express/Node.js)

```bash
nx serve backend                     # Development server
nx build backend                     # Production build
nx test backend                      # Unit tests
nx test backend --coverage          # With coverage
nx lint backend                      # ESLint
nx e2e backend-e2e                  # E2E tests
```

### Library Commands

```bash
nx test constants                    # Test constants library
nx test types                       # Test types library
nx test utils                       # Test utils library
nx lint constants                    # Lint constants library
```

### Workspace Commands

```bash
# Multi-project commands
nx run-many --target=build --all           # Build all projects
nx run-many --target=test --all            # Test all projects
nx run-many --target=lint --all            # Lint all projects

# Smart rebuilds (affected projects only)
nx affected:build                           # Build changed projects
nx affected:test                            # Test changed projects
nx affected:lint                            # Lint changed projects
nx affected:graph                           # Visualize changes

# Project generation
nx generate @nx/angular:app <app-name>      # New Angular app
nx generate @nx/express:app <app-name>      # New Express app
nx generate @nx/js:lib <lib-name>          # New TypeScript library

# Workspace utilities
nx graph                                    # Dependency graph
nx list                                     # Available plugins
nx reset                                    # Clear cache
nx migrate latest                           # Update Nx
```

## 🎭 Git Hooks \& Code Quality

### Husky Configuration

#### Pre-commit Hook

- Runs **lint-staged** on staged files
- Applies **ESLint** fixes automatically
- Formats code with **Prettier**
- Only processes files being committed (fast!)

#### Commit Message Hook

- Validates commit messages using **Commitlint**
- Enforces **Conventional Commits** specification
- Blocks commits with invalid message format

#### Pre-push Hook

- Validates branch names using **branch-name-lint**
- Skips validation for main branches (`main`, `master`, `develop`)
- Enforces consistent branch naming

### lint-staged Configuration

```json
{
  "lint-staged": {
    "*.{ts,js}": ["eslint --fix", "prettier --write"],
    "*.{html,scss,css}": ["prettier --write"],
    "*.{json,md}": ["prettier --write"]
  }
}
```

## ✨ Commitizen \& Conventional Commits

### Making Commits

```bash
# Interactive commit with Commitizen
git add .
npm run commit

# Follow the prompts:
# 1. Select commit type
# 2. Add scope (optional)
# 3. Write description
# 4. Add body (optional)
# 5. Mark breaking changes
# 6. Reference issues
```

### Commit Types

| Type         | Description         | Example                                  |
| :----------- | :------------------ | :--------------------------------------- |
| **feat**     | ✨ New features     | `feat(auth): add JWT authentication`     |
| **fix**      | 🐛 Bug fixes        | `fix(api): resolve CORS issue`           |
| **docs**     | 📚 Documentation    | `docs(readme): update setup guide`       |
| **style**    | 💄 Code formatting  | `style: apply prettier formatting`       |
| **refactor** | ♻️ Code refactoring | `refactor(utils): simplify date helpers` |
| **perf**     | ⚡ Performance      | `perf(backend): optimize queries`        |
| **test**     | 🧪 Testing          | `test(auth): add login service tests`    |
| **chore**    | 🔧 Maintenance      | `chore(deps): update Angular to v18`     |
| **ci**       | 👷 CI/CD            | `ci: add GitHub Actions workflow`        |
| **build**    | 📦 Build system     | `build: update webpack configuration`    |

### Branch Naming Convention

#### Format: `prefix/description`

```bash
# ✅ Valid Examples
feature/user-authentication
feature/shopping-cart
bugfix/login-form-validation
bugfix/memory-leak-fix
hotfix/security-vulnerability
release/v2.1.0
chore/update-dependencies
docs/api-documentation
test/e2e-user-flows
ci/github-actions-setup

# ❌ Invalid Examples
my-feature              # Missing prefix/separator
user-auth              # Missing prefix
feature-login          # Wrong separator
wip/temp-work          # Banned prefix
```

#### Valid Prefixes

- `feature/` - New features
- `bugfix/` - Bug fixes
- `hotfix/` - Critical fixes
- `release/` - Release preparation
- `chore/` - Maintenance tasks
- `docs/` - Documentation
- `test/` - Testing changes
- `ci/` - CI/CD changes

## 📚 Shared Libraries

### Constants Library (`@nx-angular-node/constants`)

```typescript
import { API_CONFIG, HTTP_STATUS } from '@nx-angular-node/constants';

// Usage example
const apiUrl = `${API_CONFIG.BASE_URL}${API_CONFIG.ENDPOINTS.AUTH}`;
```

### Types Library (`@nx-angular-node/types`)

```typescript
import { User, ApiResponse, LoginRequest } from '@nx-angular-node/types';

// Usage example
const loginData: LoginRequest = {
  email: 'user@example.com',
  password: 'password123',
};
```

### Utils Library (`@nx-angular-node/utils`)

```typescript
import { formatDate, validateEmail, debounce } from '@nx-angular-node/utils';

// Usage example
const formattedDate = formatDate(new Date());
const isValidEmail = validateEmail('user@example.com');
```

## 🛠️ Development Workflow

### Daily Development

```bash
# 1. Start development servers
npm run dev

# 2. Create feature branch
git checkout -b feature/new-dashboard

# 3. Make changes and test
nx test frontend --watch
nx lint frontend

# 4. Commit changes
git add .
npm run commit

# 5. Push branch
git push origin feature/new-dashboard
```

### Code Generation

```bash
# Generate Angular components
nx g @nx/angular:component user-profile --project=frontend

# Generate Angular services
nx g @nx/angular:service auth --project=frontend

# Generate backend routes
nx g @nx/express:route users --project=backend

# Generate shared library
nx g @nx/js:lib shared-models
```

### Testing Strategy

```bash
# Unit tests
nx test frontend                # Frontend tests
nx test backend                 # Backend tests
nx run-many --target=test --all # All unit tests

# E2E tests
nx e2e frontend-e2e            # Frontend E2E
nx e2e backend-e2e             # Backend E2E

# Test affected projects only
nx affected:test               # Smart testing
```

## 🚀 Deployment

### Build for Production

```bash
# Build all applications
npm run build:all

# Build specific applications
nx build frontend --prod
nx build backend --prod

# Check bundle sizes
nx build frontend --stats-json
```

### Environment Configuration

#### Frontend (Angular)

```typescript
// apps/frontend/src/environments/environment.prod.ts
export const environment = {
  production: true,
  apiUrl: 'https://api.yourapp.com',
};
```

#### Backend (Express)

```typescript
// apps/backend/src/environments/environment.prod.ts
export const environment = {
  production: true,
  port: process.env['PORT'] || 3333,
  database: process.env['DATABASE_URL'],
};
```

## 📊 Available Scripts

```json
{
  "scripts": {
    "dev": "npm-run-all --parallel serve:frontend serve:backend",
    "serve:frontend": "nx serve frontend",
    "serve:backend": "nx serve backend",
    "build:all": "nx run-many --target=build --all",
    "test:all": "nx run-many --target=test --all",
    "lint:all": "nx run-many --target=lint --all",
    "commit": "cz",
    "commit:retry": "cz --retry",
    "prepare": "husky",
    "format": "nx format:write",
    "graph": "nx graph"
  }
}
```

## 🔧 Troubleshooting

### Common Issues

#### Husky Hooks Failing

```bash
# Fix linting issues
nx lint --fix

# Format code
npm run format

# Skip hooks temporarily (emergency only)
git commit --no-verify
```

#### Build Issues

```bash
# Clear Nx cache
nx reset

# Clean install
rm -rf node_modules package-lock.json
npm install
```

#### Port Conflicts

```bash
# Use different ports
nx serve frontend --port 4201
nx serve backend --port 3334
```

## 🤝 Contributing

1. **Create a feature branch**: `git checkout -b feature/description`
2. **Make changes and test**: `nx affected:test && nx affected:lint`
3. **Commit using Commitizen**: `npm run commit`
4. **Push and create PR**: `git push origin feature/description`

### Code Quality Standards

- All code must pass ESLint and Prettier checks
- Maintain test coverage above 80%
- Follow conventional commit messages
- Use proper branch naming conventions

## 📄 License

This project is licensed under the MIT License.

## 📚 Resources

- [Nx Documentation](https://nx.dev/) - Nx monorepo toolkit
- [Angular Documentation](https://angular.io/) - Angular framework
- [Express.js Documentation](https://expressjs.com/) - Express.js framework
- [Conventional Commits](https://conventionalcommits.org/) - Commit specification
- [Husky Documentation](https://typicode.github.io/husky/) - Git hooks
