# AGENTS.md
# OpenCode Multi-Agent System — General Context and Rules

Configuration last updated: March 2026

## UNIVERSAL PART — DO NOT CHANGE UNLESS ABSOLUTELY NECESSARY

### Core System Operating Principles

We simulate a realistic small development team:

- **architect** — ensures long-term structural sustainability
- **planner** — breaks tasks into clear, understandable steps
- **coder** — writes and modifies code
- **reviewer** — checks code quality and architectural fit
- **tester** — adds / fixes tests
- **security** — looks for vulnerabilities
- **refactor** — improves readability and structure
- **docs** — maintains documentation
- **orchestrator** — coordinates the process and decides execution order

### Most Important General Rules (mandatory for **ALL** agents)

1. Strictly follow the rules and constraints described in the **PROJECT CONTEXT** block of the current repository
2. Code is written **for humans**, not just for machines. In 3–12 months another person (or yourself) should be able to quickly understand:
   - why this code exists
   - which important business rules / invariants / constraints are covered
   - why this particular solution was chosen (especially when it’s not the most obvious one)
   - which risks / edge cases are handled
3. Leave comments only where:
   - logic is not obvious from the code itself
   - important assumptions / pre- and post-conditions exist
   - a workaround / temporary solution is used
   - a non-standard / non-idiomatic approach is applied
   - behavior strongly depends on call order / external state
4. Good comment rules:
   - explain **WHY**, not **WHAT** (the code already shows what it does)
   - avoid obvious comments (“incrementing counter”)
   - use JSDoc / DocBlock / godoc / rustdoc / equivalent for public APIs
   - keep comments up-to-date when code changes
   - never leave outdated or contradictory comments
5. Use **Conventional Commits** for **all** commits
6. Maximum file size ~400–450 lines (except tests / generated code / data files)
7. Do **not** add new dependencies without explicit approval from architect / orchestrator
8. **Never** trust input data coming from clients / external sources

### Directory Structure (general recommendation — adapted in PROJECT CONTEXT)

project-root/
├── src/ or app/ or lib/        # main application code
├── tests/ or __tests__/        # tests
├── docs/ or architecture/      # architectural decisions, ADRs, diagrams
└── .opencode/                  # agent configuration

## GENERAL WORKFLOW (controlled by the orchestrator)

Typical sequences:

- New feature / large change  
  → architect → planner → coder → reviewer → tester → security → (refactor) → docs

- Bug fix  
  → planner → coder → tester → reviewer → security → docs

- Refactoring / code improvement  
  → planner → coder → refactor → reviewer → tester → docs

- Documentation / ADR only  
  → docs → (reviewer optional)

- Architectural discussion  
  → architect → (planner optional) → docs

The orchestrator may change order, add iterations, or introduce parallel steps when needed.

## PROJECT CONTEXT — MODIFIABLE BLOCK (change only this part for each specific project)

### Current Stack and Key Technologies

- Language(s): ___________________________
- Backend framework / runtime: _______
- Frontend (if any): ______________________
- Database / storage: ____________________
- Main libraries / tools: ________________
- Authentication: ________________________
- Testing: _______________________________
- Code style / linter / formatter: _______
- Package manager: ______________________
- CI/CD / deployment: ___________________

### Architecture and Key Principles (5–10 most important rules)

1. 
2. 
3. 
4. 
5. 
6. 
...

### Recommended Directory Structure (current as of now)

src/
├── features/ or modules/ or domains/
├── shared/ or lib/ or common/
├── ...

### Critical Prohibitions and Anti-patterns

- Never ...
- Forbidden to ...
- Access to ... is allowed only in ...
- Must not import ... into ...

### Additional Style, Patterns, and Error Handling Preferences

- Naming conventions: ...
- Error handling: ...
- Tests: ...
- Comments / documentation: ...