READ ~/work/agent/AGENTS.md BEFORE ANYTHING.

# OpenCode Configuration

**No orchestrator. Just talk to it.**

## Why No Orchestrator?

The orchestrator-first architecture is over-engineering:
- Peter Steinberger: "Don't waste time on subagents, Agents 2.0, or charades"
- Armin Ronacher: "Plan mode is just a prompt + UX"
- Simon Willison: "Senior engineers don't need orchestration theater"

Instead: Natural conversation → Implementation → Tests → Ship

## OpenCode-Specific

- Can use skills from `~/work/agent/skills/`
- RTK for token optimization (see `RTK.md`)
- Cross-reference projects with `../project-name`
- Work on main, iterate fast

## Usage

```bash
# Just talk naturally
"add login button"
"refactor auth to use tokens"
"write tests for user service"
"look at ../vibetunnel and do same for sessions"
```

No need for:
- ❌ Orchestrator delegation
- ❌ Agent spawning
- ❌ Briefing templates
- ❌ Contracts and reporting
- ❌ Quality gate ceremonies

Just:
- ✅ Short prompts
- ✅ Natural iteration
- ✅ Test in same context
- ✅ Ship

---

**Keep it simple. The model is smart enough.**
