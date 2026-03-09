# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Conventional Changelog](https://www.conventionalcommits.org/en/v1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.2.0] - 2026-03-09

### Added

- **Memory System**: Two-level memory architecture for consistent multi-task execution
  - `RUN_CONTEXT.md` - runtime memory for current task context
  - `DECISIONS.md` - permanent memory for architectural decisions
  
- **Memory Management Rules** (orchestrator.md):
  - Required reading of memory files at start of each response
  - Automatic memory updates after important steps
  - Final summary pass with extraction to permanent decisions
  - Violation detection with rollback capability

- **Quality Assurance Rules** (orchestrator.md):
  - PROJECT CONTEXT alignment check after each step
  - Quality Gate verification before proceeding
  - Final quality assessment with 1-10 score

- **5 Laws of Code** (coder.md):
  - Early Exit (Guard Clauses)
  - Parse Don't Validate
  - Atomic Predictability
  - Fail Fast, Fail Loud
  - Intentional Naming
  
- **5 Laws Checklist** (reviewer.md):
  - Explicit verification checklist for code reviews
  
- **Memory Instructions** to all agents:
  - architect.md, planner.md, coder.md, reviewer.md - full memory reading
  - tester.md, security.md - quick memory references
  - refactor.md, docs.md - DECISIONS.md mention only

- **Comprehensive README.md**:
  - PROJECT CONTEXT field explanations
  - Agent descriptions
  - Workflow documentation
  - Quick start guide

### Changed

- **AGENTS.md**:
  - Fixed agent names consistency (developer → coder, security specialist → security, etc.)
  - Added "Memory and Context" section
  - Updated workflow descriptions

- **orchestrator.md**:
  - Enhanced role description with memory management
  - Added Quality Assurance Rules section
  - Improved delegation workflow

### Fixed

- Agent name inconsistencies between AGENTS.md and .opencode/agents/ files
- Missing documentation for PROJECT CONTEXT block

## [0.1.0] - 2026-03-08

### Added

### Changed

### Deprecated

### Removed

### Fixed

### Security
