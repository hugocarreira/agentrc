# Agent Instructions

**Just talk to it.** No orchestrators, no charades, no plan mode theater.

Work style: telegraph; noun-phrases ok; drop grammar; min tokens.

---

## Core Philosophy

### Just Talk To It
- Short prompts (1-2 sentences) + screenshots
- Natural conversation, no elaborate prompts
- "give me options" when uncertain
- Iterate together, don't over-plan

### Shipping at Inference-Speed
- Expect code works out-of-the-box
- Watch the stream, don't read every line
- Trust the model when context is solid

### Blast Radius Thinking
Before starting:
- How many files will this touch?
- How long should this take?
- Can this run in parallel?

If stuck, ESC + "what's the status"

---

## What Actually Works (Senior Engineering Practices)

### Automated Testing
- Tests for all business logic (unit + integration)
- **Write tests in same context** as implementation (finds bugs automatically!)
- Test-first when possible
- No flaky tests

### Documentation
- Keep `docs/` folder with frontmatter (`summary`, `read_when`)
- Update docs for user-facing changes
- Inline comments for tricky/bug-prone logic
- README for onboarding

### Version Control
- Conventional Commits (`feat:`, `fix:`, `refactor:`, `chore:`, `docs:`)
- Atomic commits (one logical change)
- Only push when asked
- No force push without permission
- Use `git bisect` when hunting bugs

### Planning (Simple)
- Start with conversation, ask clarifying questions
- Write to `docs/*.md` if complex
- Iterate on plan before building
- Don't over-plan, iterate fast

### Cross-Reference Projects
```bash
"look at ../other-project and do the same"
"check how we solved X in ../vibetunnel"
```
Model is great at reusing patterns.

### CLI-First
- Start with CLI, build UI later
- Easier to test, model can verify output
- Closes the loop faster

---

## Workflow

### Iterate Fast, Refactor Smart
- **80% building** → **20% refactoring**
- Work on `main` by default (no worktrees unless asked)
- Refactor when prompts get slow
- Commit atomically after each feature

### Code Quality
- TypeScript strict mode, no `any` without justification
- Proper error handling (never swallow)
- No secrets in code (env vars only)
- No `console.log` in production

### Prompting
- Short prompts + screenshots (~50% should include images)
- Show don't tell: `[screenshot] "fix padding"`
- Trigger words for hard tasks: "take your time", "comprehensive", "read all related code"

---

## Tools & Efficiency

### RTK - Token Killer
**Always prefix shell commands with `rtk`**

```bash
rtk git status
rtk npm test
rtk cargo build
```

See `RTK.md` for full reference.

### CLIs > MCPs
Prefer CLIs with good help menus:
- `gh` (GitHub)
- `vercel` (deploy)
- `psql` (database)
- `bun` (JavaScript runtime)

MCPs pollute context. Only use when no CLI exists.

### Skills Discovery
32 skills available in `skills/` folder:
- Development: `commit-and-push`, `pullrequest`, `test-and-verify`
- Frontend: `frontend-design`, `accessibility`, `core-web-vitals`
- Next.js: `next-best-practices`, `next-upgrade`
- SEO: `seo`, `seo-audit`, `programmatic-seo`
- Product: `product-strategy`, `page-cro`, `signup-flow-cro`

Skills auto-trigger on relevant keywords. List with `ls ~/work/agent/skills/`

---

## Bash Safety

### NEVER (without explicit permission):
- `rm -rf` outside project
- `sudo` anything
- `git push --force` to main
- `npm publish`, `docker push`
- `curl | bash` patterns

### ALWAYS prefer:
- Read-only commands first (`ls`, `rtk grep`, `rtk find`)
- Scoped commands (`npm test`, not `npm run all`)
- Dry-run flags (`terraform plan`)

---

## Project Context

### Read First
1. Project's `AGENTS.md` (if exists)
2. Relevant existing code (understand patterns)
3. `docs/` folder (check frontmatter `read_when`)

### Per-Project AGENTS.md Template
```markdown
READ ~/work/agent/AGENTS.md BEFORE ANYTHING.

# [Project Name]

## Stack
- Language: TypeScript/Go/Python
- Framework: Next.js/Gin/FastAPI
- Database: PostgreSQL/MongoDB

## Conventions
- Package manager: bun/pnpm/npm
- Test command: `bun test`
- Lint: `bun run lint`

## Out of Scope
- Never touch `lib/billing/` (legacy)
```

---

## What NOT to Do

❌ **No orchestrators** - Talk directly, no delegation theater
❌ **No plan mode charades** - Just write to `docs/*.md` if needed
❌ **No RAG systems** - Model can search fine
❌ **No subagent spawning** - Keep it simple
❌ **No elaborate prompts** - Short and natural
❌ **No over-planning** - Iterate and ship

---

## Error Recovery

1. **Self-fix** - Read error, fix once (ONE attempt)
2. **Simplify** - Strip to minimal reproduction
3. **Stop and report**:
   ```
   ❌ BLOCKED
   Task: [what I was doing]
   Error: [exact message]
   Tried: [fix attempts]
   Assessment: [what I think is wrong]
   ```
4. **Ask user** - Only after 2 failed attempts

Never retry same fix twice. Never swallow errors.

---

## Mental Model

```
User
  ↓ (short prompt + maybe screenshot)
Agent (reads this file + RTK.md + project AGENTS.md + docs/)
  ↓ (understands context, reads relevant code)
  ↓ (implements, tests in same session)
  ↓ (atomic commit)
Result
```

No layers. No delegation. No theater.

**The model is smart. Talk to it like a senior engineer.**

---

## Summary

- Just talk to it (no charades)
- Test in same context (finds bugs)
- Cross-reference projects (reuse patterns)
- CLIs > MCPs (less context pollution)
- RTK everything (token efficiency)
- Iterate fast, refactor smart (80/20)
- Commit atomically (conventional commits)
- Read docs first, update docs after

**That's it. Keep it simple.**

---

_Based on workflows from [Peter Steinberger](https://steipete.me), [Simon Willison](https://simonwillison.net), and [Armin Ronacher](https://lucumr.pocoo.org)._
