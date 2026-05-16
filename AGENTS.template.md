READ ~/work/agent/AGENTS.md BEFORE ANYTHING.

# [Project Name]

## Stack
- Language: TypeScript/Go/Python
- Framework: Next.js/Gin/FastAPI
- Database: PostgreSQL/MongoDB
- Package manager: bun/pnpm/npm

## Test & Build Commands
```bash
rtk bun test           # Run tests
rtk bun run lint       # Lint
rtk bun run build      # Build
```

## Conventions
- API routes in: `app/api/` or `src/routes/`
- Components in: `components/` or `src/components/`
- Naming: camelCase for functions, PascalCase for components

## Out of Scope
- Never modify: `lib/billing/` (legacy system, don't touch)
- Never touch: `config/secrets/` (managed separately)

## Project-Specific Patterns
[Add any specific patterns, preferences, or quirks of this project]

---

**Keep simple. Just talk to the model.**
