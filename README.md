# OpenCode Multi-Agent System Template

A comprehensive template for setting up an OpenCode multi-agent development team. This template provides a structured approach to coordinating multiple AI agents for software development tasks, with clear roles, workflows, and best practices.

## Introduction

This project serves as a **template** for implementing the OpenCode Multi-Agent System. It provides the foundational configuration and agent definitions that teams can customize for their specific project needs.

The system simulates a realistic small development team with specialized agents, each having distinct responsibilities:

- **Architect** — ensures long-term structural sustainability
- **Planner** — breaks tasks into clear, understandable steps
- **Coder** — writes and modifies code
- **Reviewer** — checks code quality and architectural fit
- **Tester** — adds and fixes tests
- **Security** — looks for vulnerabilities
- **Refactor** — improves readability and structure
- **Docs** — maintains documentation
- **Orchestrator** — coordinates the process and decides execution order

The orchestrator acts as the team lead, analyzing user requests and delegating tasks to the appropriate agents in the correct sequence.

## Quick Start

To start using this template for your project:

1. **Clone or copy** this template repository to your local machine
2. **Customize AGENTS.md** — Fill in the PROJECT CONTEXT block (lines 78-120) with your specific project details
3. **Configure agents** — Review and modify agent definitions in `.opencode/agents/` as needed
4. **Set up your project** — Initialize your actual project code in the appropriate directories
5. **Run OpenCode** — Start using OpenCode with this configuration to develop your project

No additional installation is required beyond having OpenCode properly installed. The agent configuration is automatically loaded from the `.opencode/` directory.

## PROJECT CONTEXT Explanation

The PROJECT CONTEXT block (lines 78-120 in AGENTS.md) is the most important section to customize for your specific project. It provides all agents with essential context about your technology stack, architecture, and coding standards.

### Current Stack and Key Technologies

This section defines the technology stack used in your project. Each field should be filled with your specific technology choices:

- **Language(s)** — The primary programming languages used (e.g., TypeScript, Python, Go, Rust)
- **Backend framework / runtime** — The web framework or server runtime (e.g., Express, Fastify, Django, Next.js, Node.js)
- **Frontend** — The UI framework if applicable (e.g., React, Vue, Svelte, Next.js)
- **Database / storage** — The database system used (e.g., PostgreSQL, MongoDB, MySQL, Redis)
- **Main libraries / tools** — Key dependencies and tools (e.g., tRPC, Prisma, Tailwind CSS)
- **Authentication** — The authentication solution (e.g., next-auth, Clerk, Lucia, JWT, OAuth)
- **Testing** — Test frameworks used (e.g., Jest, Vitest, Playwright, Cypress)
- **Code style / linter / formatter** — Linting and formatting tools (e.g., ESLint, Prettier, Ruff, black)
- **Package manager** — The package manager used (e.g., npm, pnpm, yarn, bun)
- **CI/CD / deployment** — Deployment platform and CI/CD pipeline (e.g., GitHub Actions, GitLab CI, Vercel, Docker)

**Example:**

```markdown
- Language(s): TypeScript, Python
- Backend framework / runtime: Fastify, Node.js
- Frontend: React, Next.js
- Database / storage: PostgreSQL, Redis
- Main libraries / tools: tRPC, Prisma, Tailwind CSS, Zod
- Authentication: next-auth
- Testing: Vitest, Playwright
- Code style / linter / formatter: ESLint, Prettier
- Package manager: pnpm
- CI/CD / deployment: GitHub Actions, Vercel
```

### Architecture and Key Principles

This section contains 5-10 critical rules that all agents must follow when working on your project. These principles guide architectural decisions and ensure consistency across the codebase.

Each rule should be a concise statement that defines a key architectural principle or constraint:

```markdown
1. Business logic must be in server/ modules only
2. All API endpoints must use tRPC procedures in features/*/server/
3. Components must be in features/*/components/
4. Shared utilities must be in lib/ directory
5. All data validation must use Zod schemas
6. Database access must go through Prisma client only
```

These rules help agents understand the project structure and make consistent decisions without needing constant guidance.

### Recommended Directory Structure

This section defines the suggested folder organization for your project. The structure should reflect your architecture principles and make it easy to locate code.

```markdown
src/
├── features/ or modules/ or domains/  # Feature-specific code
├── shared/ or lib/ or common/          # Shared utilities and libraries
├── server/                             # Server-side business logic
├── components/                        # Reusable UI components
├── ...
```

**Example for a typical project:**

```markdown
src/
├── features/
│   ├── auth/
│   │   ├── components/
│   │   ├── server/
│   │   └── index.ts
│   ├── users/
│   └── posts/
├── lib/
│   ├── db.ts
│   └── utils.ts
├── server/
│   └── router.ts
└── app/
```

This organization keeps related code together and separates concerns effectively.

### Critical Prohibitions and Anti-patterns

This section explicitly lists restrictions and anti-patterns that agents must avoid. These are hard rules that should never be violated:

```markdown
- Never store secrets in code (use environment variables)
- Forbidden to commit directly to main branch
- Access to database must be allowed only through Prisma client
- Must not import server/ code into client components
- Never skip input validation on API endpoints
```

Defining these prohibitions helps prevent common mistakes and security vulnerabilities.

### Additional Style, Patterns, and Error Handling Preferences

This section provides detailed guidance on coding conventions and patterns:

- **Naming conventions** — Defines the case style for different code elements (e.g., camelCase for variables, PascalCase for classes, snake_case for database tables)
- **Error handling** — Specifies how errors should be managed (e.g., try-catch blocks, Result types, error boundaries)
- **Tests** — Defines test naming patterns and coverage requirements (e.g., tests should be named `shouldXWhenY`)
- **Comments / documentation** — Specifies JSDoc requirements and when comments are required

**Example:**

```markdown
- Naming conventions: camelCase (variables), PascalCase (components), snake_case (database)
- Error handling: Use Result types for recoverable errors, throw for critical failures
- Tests: Name format shouldXWhenY (e.g., shouldReturnUserWhenIdExists)
- Comments: JSDoc required for all public functions, explain WHY not WHAT
```

## Agent Files

Each agent is defined in `.opencode/agents/` with specific responsibilities and rules. Here's a brief description of each:

### architect.md

Evaluates task impact on project architecture, defines module boundaries and dependencies, suggests patterns for complex tasks, and analyzes existing structure. Does not write code—only makes architectural decisions.

### planner.md

Analyzes task requirements, creates step-by-step implementation plans, determines execution order, and identifies dependencies between tasks. Produces plans without writing code.

### coder.md

Implements features, fixes bugs, and refactor code following project architecture and conventions. Writes clean, maintainable code with appropriate comments explaining complex logic, workarounds, and important assumptions.

### reviewer.md

Checks code against standards, finds potential issues, and suggests improvements. Does not modify code directly but identifies problems and suggests specific fixes. Ensures adequate documentation and comments exist.

### tester.md

Writes unit and integration tests, fixes existing tests, and checks code test coverage. Names tests using the `shouldXWhenY` pattern and tests critical scenarios.

### security.md

Scans for vulnerabilities, checks input data security, analyzes authentication and authorization, and ensures protection against common vulnerabilities (SQL injection, XSS, CSRF). Ensures secrets are never stored in code.

### refactor.md

Improves code structure without changing behavior, eliminates duplication, optimizes performance, and simplifies complex code. Makes small, safe changes following SOLID principles.

### docs.md

Writes and updates JSDoc for public functions, types, and tRPC procedures. Creates README files for features, writes Architectural Decision Records (ADRs), generates Mermaid diagrams, and maintains CHANGELOG.md.

### orchestrator.md

Coordinates the entire agent team. Analyzes user requests, determines task type, delegates to sub-agents in logical sequence, and handles results. Ensures proper workflow execution and final reporting to the user.

## Workflows

The orchestrator manages different workflows based on the type of task:

### New Feature / Major Change

```
architect → planner → coder → reviewer → tester → security → refactor (optional) → docs
```

Used for implementing significant new functionality that requires architectural planning.

### Bug Fix

```
planner → coder → tester → reviewer → security → docs
```

Used for fixing bugs, typically starting with planning the fix, implementing it, testing, and reviewing.

### Refactoring / Code Improvement

```
planner → coder → refactor → reviewer → tester → docs
```

Used for improving code structure, eliminating duplication, or optimizing performance without changing behavior.

### Documentation Only / ADR

```
docs → reviewer (optional)
```

Used for documentation updates or creating Architectural Decision Records.

### Architecture Discussion / Design

```
architect → (planner optional) → docs
```

Used for discussing architectural decisions or design patterns before implementation.

The orchestrator may modify these workflows based on task complexity, adding iterations or parallel steps as needed.
