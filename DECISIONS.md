# DECISIONS.md — Project-Specific Decisions

All general rules, workflow, and agent responsibilities are defined in **AGENTS.md**.
This file contains only project-specific architectural decisions.

# Architectural and Key Project Decisions

(This file is permanent — decisions here take priority over everything else)

## Date · Decision · Agent Author

## 2026-04-08 · Orchestrator role: verify, not write · Orchestrator
- Context: Orchestrator had write: false in opencode.json but its prompt said to write to DECISIONS.md and RUN_CONTEXT.md
- Decision: Orchestrator does NOT write to memory files. Instead, it VERIFIES that agents (Architect, Planner, Coder) wrote to their respective files. If agent didn't write — do not call next agent.
- Reasoning: Orchestrator's role is to coordinate and verify, not to implement. Writing should be done by the agent responsible for that stage.

## 2026-04-08 · All agents must read project memory · Orchestrator
- Context: docs.md, tester.md, and security.md did not read required memory files before starting work
- Decision: Every agent must read DECISIONS.md, RUN_CONTEXT.md, and (where applicable) CODER_DECISIONS.md before starting work. This is mandatory for all agents.
- Reasoning: Without reading memory, agents work blind and may contradict previous decisions.

## 2026-04-08 · Unified English language for all prompts · Orchestrator
- Context: Agent prompts contained mixed Russian and English ("обязательно прочитай")
- Decision: All agent prompts must be in English only. No exceptions.
- Reasoning: Mixed languages confuse LLMs and reduce output quality.

## 2026-04-08 · Project-specific rules belong in PROJECT_CONTEXT.md · Orchestrator
- Context: coder.md and docs.md contained project-specific rules (tRPC, features/*, server/) that are not universal
- Decision: Project-specific architecture rules (directory structure, framework conventions) belong in PROJECT_CONTEXT.md. Agent prompts must reference PROJECT_CONTEXT.md, not hardcode project rules.
- Reasoning: Prompts should be reusable across projects. Only PROJECT_CONTEXT.md should change per project.

## 2026-04-08 · Every agent must have Output Format · Orchestrator
- Context: Most agents had no defined output format, leading to unpredictable responses
- Decision: Every agent must include an Output Format section describing the expected structure of their response to the Orchestrator.
- Reasoning: Structured output ensures Orchestrator can properly interpret agent results and make routing decisions.

## 2026-04-08 · Orchestrator delegates all file writes · Orchestrator
- Context: Orchestrator.md contained instructions to write to files (Retry Tracking, archive creation) but Orchestrator has write: false
- Decision: Orchestrator never writes to files directly. All file writes are delegated: Planner writes to RUN_CONTEXT.md, Architect writes to DECISIONS.md, Coder writes to CODER_DECISIONS.md. Orchestrator only verifies writes were completed.
- Reasoning: Consistent with Orchestrator's role as coordinator, not implementer.

## 2026-04-08 · All agents read CODER_DECISIONS.md · Orchestrator
- Context: architect.md and planner.md did not read CODER_DECISIONS.md, missing important technical context during iterations
- Decision: All agents must read CODER_DECISIONS.md before starting work, not just coder and reviewer.
- Reasoning: During iterative workflows (reviewer finds issues → coder fixes → architect/planner re-evaluate), architect and planner need to know what technical decisions coder made.

## 2026-04-08 · Parallel execution only after reviewer APPROVE · Orchestrator
- Context: feature-development.md allowed reviewer + security to run in parallel, but if reviewer requests changes, security checks outdated code
- Decision: Reviewer and security can only run in parallel if reviewer has APPROVED the code with no changes requested. If reviewer requests changes, security must wait until coder fixes and reviewer re-approves.
- Reasoning: Prevents security from checking code that will be modified based on reviewer feedback.

## 2026-04-08 · AGENTS.md reflects Planner as RUN_CONTEXT manager · Orchestrator
- Context: AGENTS.md stated "RUN_CONTEXT.md managed by Orchestrator" but Orchestrator doesn't write to files
- Decision: RUN_CONTEXT.md is managed by Planner and verified by Orchestrator. Feedback from agents is reported to Orchestrator, who instructs Planner to update RUN_CONTEXT.md.
- Reasoning: Consistent with the decision that Orchestrator coordinates but does not write.

## 2026-04-08 · Migrated opencode.json from deprecated tools to permissions · Orchestrator
- Context: OpenCode documentation states that "tools" field is deprecated in favor of "permission" field. The old boolean format (write: true/false, edit: true/false, bash: true/false) has been replaced with the new string format (edit: "allow"/"deny", bash: "allow"/"deny").
- Decision: Migrated all agent configurations from `tools` to `permission` format. Orchestrator now has `task: { "*": "allow" }` permission to invoke all subagents. Removed `write` permission (merged into `edit`). Added `task` permissions only for orchestrator.
- Reasoning: Following OpenCode's current API conventions. The `permission` format is more granular (supports "ask"/"allow"/"deny") and is the officially supported way forward.

## 2026-04-08 · Granular permissions for all agents · Orchestrator
- Context: Migrated from deprecated `tools` to `permissions`, expanded with granular `bash`, `webfetch`, `websearch`, `skill` permissions
- Decision: Each agent has carefully scoped permissions based on its role. Global `git push` denied for all agents. Coder and tester have `rm` denied. Read-only agents (reviewer, security) can only run git read commands. All agents can use `skill` and `webfetch`. Task permission only for orchestrator.
- Reasoning: Least privilege principle — agents should only access what they need for their role. Git push is user-only. Dangerous commands like `rm` are denied even for code-writing agents.

## 2026-04-08 · Task permission only for orchestrator · Orchestrator
- Context: Considered giving coder ability to call tester directly for faster iteration
- Decision: Keep `task` permission only for orchestrator. All subagent orchestration goes through orchestrator.
- Reasoning: Single coordinator ensures predictable workflow, retry limits work correctly, quality gates are enforced, and memory management is consistent. Subagents can't bypass the orchestrator's verification steps.
