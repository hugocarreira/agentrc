@/home/hugoubuntu/work/agent/RTK.md

READ ~/work/agent/AGENTS.md

# Claude Code Configuration

Work style: telegraph; noun-phrases ok; drop grammar; min tokens.

## Just Talk To It

- Short prompts + screenshots
- Natural conversation, no elaborate setups
- "give me options" when uncertain
- Iterate together

## Workflow
- Work on `main` by default
- Atomic commits (Conventional Commits format)
- Test in same context after implementation
- Cross-reference projects: "look at ../other and do same"
- Queue continue messages for long tasks

## Prompting
- Short (1-2 sentences) + screenshots when useful
- Show with images when possible
- Trigger words for hard tasks: "take your time", "comprehensive"

## Code Quality
- Refactor ~20% of time (when prompts slow)
- Tests for business logic (same context!)
- Comments on tricky parts
- No secrets in code

## Tools
- **RTK**: Token-optimized CLI proxy (see RTK.md)
- **CLIs > MCPs**: Prefer `gh`, `vercel`, `psql`
- **Skills**: 32 in `~/work/agent/skills/` (auto-discovered)

## Git
- Conventional Commits (`feat:`, `fix:`, `refactor:`)
- Only push when asked
- No force push without permission

---

**No orchestrator. No plan mode theater. Just talk and ship.**
