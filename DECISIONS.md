### Workflow Order (MANDATORY)
```
New feature / major change:
architect → planner → coder → reviewer → tester → security → docs

Bugfix:
planner → coder → tester → reviewer → security → docs
```

### Agent Responsibilities
| Agent | Writes to | Reads |
|-------|-----------|-------|
| **Architect** | DECISIONS.md | - |
| **Planner** | RUN_CONTEXT.md | DECISIONS.md |
| **Coder** | CODE + docs/CODER_DECISIONS.md | DECISIONS.md, RUN_CONTEXT.md |
| **Reviewer** | - | CODE |
| **Tester** | Tests | CODE |
| **Security** | - | CODE |
| **Docs** | Documentation | - |

### Coder Decision Log
- **File**: `docs/CODER_DECISIONS.md`
- **Who Writes**: Coder
- **Who Reads**: All agents before starting work (in addition to DECISIONS.md/RUN_CONTEXT.md)
- **Purpose**: Technical decisions, rejected approaches, workarounds, lessons learned
- **What to record**:
  - Rejected approaches and why
  - Workarounds and their limitations  
  - Technical trade-offs
  - Lessons learned ("gotchas")
- **Format**: Date + Author + Context + Decision + Outcome + Reasoning
- **Why**: Prevents repeating mistakes in future iterations

### Critical Rules
1. **General agent is NOT ALLOWED for development** - Only use for research/exploration
2. **Broken agent = STOP** - Do NOT skip to next agent, wait for fix
3. **No skipping stages** - Always follow workflow order
4. **Memory files** - Architect writes to DECISIONS.md, Planner to RUN_CONTEXT.md, Coder does NOT write to DECISIONS.md

### If Agent Fails
- Report the error to user
- DO NOT proceed to next agent
- DO NOT use General as substitute
- Wait for configuration fix


# Architectural and Key Project Decisions

(This file is permanent — decisions here take priority over everything else)

## Date · Decision · Agent Author
