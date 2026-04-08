# AGENTS.md
# OpenCode Multi-Agent System — General Context and Rules

Configuration last updated: March 2026

## UNIVERSAL PART — DO NOT CHANGE UNLESS ABSOLUTELY NECESSARY

### Core System Operating Principles

We simulate a realistic small development team:

You are Orchestrator — the coordinator of the entire agent team.

- **orchestrator** — coordinates the process and decides execution order
- **architect** — ensures long-term structural sustainability
- **planner** — breaks tasks into clear, understandable steps
- **coder** — writes and modifies code
- **reviewer** — checks code quality and architectural fit
- **tester** — adds / fixes tests
- **security** — looks for vulnerabilities
- **docs** — maintains documentation

### Agents directory Structure

project-root/
├── src/ or app/ or lib/        # main application code
├── tests/ or __tests__/        # tests
├── docs/ or architecture/      # architectural decisions, ADRs, diagrams
└── .opencode/                  # agent configuration
    ├── agents/                 # agent configurations
    │   ├── orchestrator.md     # orchestrator agent
    │   ├── planner.md         # planner agent
    │   ├── architect.md       # architect agent
    │   ├── coder.md           # coder agent
    │   ├── reviewer.md        # reviewer agent
    │   ├── tester.md          # tester agent
    │   ├── security.md        # security agent
    │   └── docs.md            # docs agent
    └── workflows/              # workflow templates
        └── feature-development.md


### Critical Rules (mandatory for **ALL** agents)

1. Strictly follow the rules and constraints described in **PROJECT_CONTEXT.md** (the PROJECT CONTEXT block)
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
9. **General agent is NOT ALLOWED for development** - Only use for research/exploration
10. **Broken agent = STOP** - Do NOT skip to next agent, wait for fix
11. **No skipping stages** - Always follow workflow order
12. **Memory files** - Architect writes to DECISIONS.md, Planner to RUN_CONTEXT.md, Coder does NOT write to DECISIONS.md

## GENERAL WORKFLOW (controlled by the orchestrator)

Typical sequences:

- New feature / large change  
  → architect → planner → coder → reviewer → tester → security → docs

- Bug fix  
  → planner → coder → tester → reviewer → security → docs

- Documentation / ADR only  
  → docs → (reviewer optional)

- Architectural discussion  
  → architect → (planner optional) → docs

The orchestrator may change order, add iterations, or introduce parallel steps when needed.

### Iterative Workflow (EXTENDS GENERAL WORKFLOW)
Orchestrator controls the process after each agent:
```
1. Agent does the work
2. Orchestrator checks results:
   ✓ No issues → next agent
   ✗ Has issues → return to Coder for fixes
3. Coder fixes → returns to Agent for re-check
4. Repeat until all agents approve
```

#### Iteration Rules:
- **Reviewer** → found issues → Coder fixes → Reviewer checks again
- **Tester** → found bugs → Coder fixes → Tester checks again
- **Security** → found vulnerabilities → Coder fixes → Security checks again
- Only after all agents approve → move to next

### Feedback Loop (MANDATORY)
When Agent finds issues → follow Iteration Rules above. Report feedback to Orchestrator, who instructs Planner to update RUN_CONTEXT.md.

### Coder Decision Log (MANDATORY)
- **File**: `docs/CODER_DECISIONS.md`
- **When**: Coder records decisions IMMEDIATELY when made, not at the end
- **Who Reads**: All agents BEFORE starting work (must read AGENTS.md, PROJECT_CONTEXT.md, DECISIONS.md, RUN_CONTEXT.md)
- **Purpose**: Transparency of thinking for other agents
- **What to record**:
  - Rejected approaches and why
  - Workarounds and their limitations
  - Technical trade-offs
  - Lessons learned ("gotchas")
  - Fixes based on Tester/Security/Reviewer feedback
- **Format**: Date + Author + Context + Decision + Outcome + Reasoning

---

## Memory and Context

All agents must read these files before starting work:

| File | Purpose |
|------|---------|
| **AGENTS.md** | Universal rules, workflow, agent responsibilities |
| **PROJECT_CONTEXT.md** | Project-specific context (stack, principles, structure) — FILLED BEFORE EACH PROJECT |
| **DECISIONS.md** | Project-specific architectural decisions |
| **RUN_CONTEXT.md** | Current task progress and context (managed by Planner, verified by Orchestrator) |

**Priority**: AGENTS.md → PROJECT_CONTEXT.md → DECISIONS.md → RUN_CONTEXT.md

These files help maintain consistency across task sessions and prevent conflicting decisions.