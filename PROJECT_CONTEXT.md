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

- Business logic → ONLY in server/ modules (never in client components)
- tRPC procedures → ONLY in features/*/server/
- README.md for features → create inside features/[feature-name]/
- Never store secrets in code — use environment variables
- Never trust input data from clients / external sources
- Must not import server code into client code directly

### Additional Style, Patterns, and Error Handling Preferences

- Naming conventions: follow PROJECT_CONTEXT.md language conventions
- Error handling: fail fast with descriptive error messages
- Tests: naming pattern shouldXWhenY
- Comments / documentation: explain WHY, not WHAT; JSDoc on public APIs