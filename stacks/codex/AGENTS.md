@/home/hugoubuntu/work/agent/RTK.md

READ ~/work/agent/AGENTS.md

# Codex Configuration

Work style: telegraph; noun-phrases ok; drop grammar; min tokens.

## Peter Steinberger Workflow

### Core Principles
- **Just Talk To It**: Short prompts (1-2 sentences) + screenshots
- **Shipping at Inference-Speed**: Expect one-shot success
- **Blast Radius Thinking**: Know impact before starting
- **Iterate Fast**: 80% building, 20% refactoring

### Workflow
- Work on `main` (no worktrees unless asked)
- Atomic commits per feature
- Test in same context (finds bugs automatically)
- Cross-reference: "look at ../project and do same"
- Queue continue messages for long tasks

### Prompting
- Short + screenshots (~50% include images)
- "give me options before making changes" for big tasks
- Show don't tell: `[screenshot] "fix padding"`

### Code Quality
- Refactor when prompts slow (~20% of time)
- Inline comments for tricky parts
- Tests after each feature (same context!)

### Tools
- **RTK**: Always prefix shell commands (see RTK.md)
- **CLIs > MCPs**: `gh`, `vercel`, `psql`, `bun`
- **Skills**: 32 available in `~/work/agent/skills/`

---

**No orchestrators. No plan mode theater. Just ship.**
