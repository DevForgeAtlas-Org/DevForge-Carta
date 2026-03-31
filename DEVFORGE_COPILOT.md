# DEVFORGE for GitHub Copilot
# File: .github/copilot-instructions.md
# Copilot reads this for all suggestions and code reviews in this repo.
# Generated: 2026-03-27
# Home: DevForgeAtlas-Org/DevForge-Atlas
# Source: packages/standalone/DEVFORGE_COPILOT.md

## Code Generation Standards

When generating code, always:
- Place business logic in service layer only — never in routes or repositories
- Place DB queries in repository layer only — never in services
- Inject dependencies via constructor — never import concrete classes directly
- Use async/await for all I/O — never callbacks or .then() chains
- Add explicit return type annotations on all functions
- Handle all errors with try/catch — log with context (requestId, userId), never swallow

## TypeScript Rules
- No `any` — use `unknown` and type-narrow
- All interfaces exported from `types.ts` collocated with the feature
- Discriminated unions for domain models, not class hierarchies
- All async functions return `Promise<T>` explicitly typed

## File Structure
When generating new features, use this structure:
```
src/features/{feature}/
  {feature}.routes.ts      # HTTP only — no business logic
  {feature}.service.ts     # Business logic only — no DB calls
  {feature}.repository.ts  # DB only — no business logic
  {feature}.types.ts       # Types and interfaces
  {feature}.test.ts        # Tests collocated
```

## Security
- Add auth middleware to EVERY new route — no exceptions
- Validate and sanitise all input parameters
- Never suggest hardcoded credentials, API keys, or secrets
- Use parameterised queries — never string interpolation in SQL

## Testing
- Test files collocated: `feature.test.ts` next to `feature.ts`
- One describe block per function/method
- Test names: "should [expected outcome] when [condition]"
- Mock all external dependencies (DB, APIs, services)
- Test error cases, not just happy path

## PR Reviews
Flag these as required changes:
- Missing auth checks on routes
- Business logic in routes or repositories
- Hardcoded credentials or secrets
- Unbounded list queries (missing pagination)
- Error handlers that log nothing or swallow errors
- `any` types without explanation

## Never Generate
- Code that bypasses auth middleware
- SQL queries without parameterisation
- Synchronous file I/O in request handlers
- console.log in production code paths (use structured logging)
- Direct DB calls from service layer
