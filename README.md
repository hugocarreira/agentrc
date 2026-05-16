# 🤖 AI Agent Configuration

**Single source of truth for OpenCode, Codex, and Claude Code**

**Philosophy**: Just talk to it. No orchestrators, no charades, no plan mode theater.

---

## 📁 Structure

```
~/work/agent/
├── AGENTS.md              # Core rules (simple!)
├── RTK.md                 # Token optimization
├── AGENTS.template.md     # Template for projects
│
├── skills/                # 32 reusable workflows
│   ├── commit-and-push/
│   ├── test-and-verify/
│   ├── frontend-design/
│   └── ... (29 more)
│
├── plugins/              
│   └── rtk.ts            # RTK plugin
│
├── docs/
│   ├── shipping-checklist.md
│   └── refactoring-guide.md
│
├── stacks/               # Stack-specific configs
│   ├── opencode/AGENTS.md
│   ├── codex/AGENTS.md
│   └── claude/CLAUDE.md
│
└── setup-symlinks.sh     # Auto-setup
```

---

## 🚀 Quick Setup

```bash
cd ~/work/agent
./setup-symlinks.sh
```

This creates symlinks:
```
~/.config/opencode/AGENTS.md → ~/work/agent/stacks/opencode/AGENTS.md
~/.codex/AGENTS.md           → ~/work/agent/stacks/codex/AGENTS.md
~/.claude/CLAUDE.md          → ~/work/agent/stacks/claude/CLAUDE.md

All skills:                  → ~/work/agent/skills/
```

---

## 🎯 Philosophy

### What This IS
✅ **Simple, direct rules** based on what actually works
✅ **Senior engineering practices** (tests, docs, git, planning)
✅ **Just talk to it** - short prompts, natural conversation
✅ **Token efficiency** - RTK everywhere
✅ **Cross-reference** - reuse patterns from other projects
✅ **Iterate fast** - 80% building, 20% refactoring

### What This IS NOT
❌ **No orchestrator** - no delegation theater
❌ **No plan mode charades** - just write to `docs/*.md` if needed
❌ **No RAG systems** - model searches fine
❌ **No subagent spawning** - keep it simple
❌ **No elaborate prompts** - short and effective
❌ **No over-engineering** - KISS principle

---

## 💡 Core Principles

### Just Talk To It (Peter Steinberger)
```bash
# ✅ Good
"add login button"
"look at ../vibetunnel and do same for sessions"
[screenshot] "fix this padding"

# ❌ Over-engineered
"I need you to carefully analyze the authentication system,
decompose the task into subtasks, delegate to specialized agents..."
```

### Shipping at Inference-Speed
- Expect code works out-of-the-box (one-shot)
- Watch the stream, don't read every line
- Trust when context is solid

### Blast Radius Thinking
Before starting:
- How many files?
- How long?
- Parallel or sequential?

### What Actually Works (Simon Willison)
Senior engineering practices that LLMs amplify:
- **Automated testing** (write in same context!)
- **Good documentation** (`docs/` folder)
- **Version control** (atomic commits)
- **Planning** (simple, iterative)
- **Code review** culture
- **Manual QA** skills
- **Research** abilities

---

## 🛠️ Usage

### Daily Workflow
```bash
# Start naturally
"implement user auth"

# Model reads:
# 1. ~/work/agent/AGENTS.md (core rules)
# 2. ~/work/agent/RTK.md (token optimization)
# 3. Project's AGENTS.md (if exists)
# 4. Relevant code

# Implements → Tests (same context!) → Commits
```

### Cross-Reference Projects
```bash
"look at ../other-project and do the same"
"check how we solved X in ../vibetunnel"
```

Model is excellent at reusing patterns.

### Add to Projects
```bash
cd ~/work/my-project
cp ~/work/agent/AGENTS.template.md AGENTS.md
# Edit with project specifics
```

---

## 📊 What's Included

### 32 Skills (All Stacks)
**Development**: commit-and-push, pullrequest, test-and-verify, frontend-design, best-practices

**Next.js**: next-best-practices, next-cache-components, next-upgrade

**SEO/Marketing**: seo, seo-audit, programmatic-seo, marketing-ideas

**Product/CRO**: page-cro, signup-flow-cro, onboarding-cro, product-strategy

**Design/Performance**: premium-saas-design, accessibility, core-web-vitals

**+ 17 more** in `skills/` folder

### Stack Behaviors

**OpenCode**: No orchestrator, just direct conversation + skills

**Codex**: Peter Steinberger workflow (short prompts + screenshots)

**Claude**: Conversational iteration, queue continue messages

All share: RTK, skills, core principles

---

## 🔧 Maintenance

### Update Global Rules
```bash
nano ~/work/agent/AGENTS.md
git commit -am "refactor: simplify X"
```
✅ All stacks see the change

### Add New Skill
```bash
mkdir ~/work/agent/skills/my-workflow
nano ~/work/agent/skills/my-workflow/SKILL.md
```
✅ Auto-discovered by all harnesses

### Stack-Specific Tweak
```bash
nano ~/work/agent/stacks/{opencode,codex,claude}/*.md
```

### Re-run Setup
```bash
./setup-symlinks.sh  # Safe, auto-backs up
```

---

## 📝 Project Template

```markdown
READ ~/work/agent/AGENTS.md BEFORE ANYTHING.

# My Project

## Stack
- TypeScript + Next.js 15
- PostgreSQL + Prisma
- Tailwind CSS

## Commands
- Test: `bun test`
- Lint: `bun run lint`
- Dev: `bun dev`

## Conventions
- Use `bun` not `npm`
- API routes in `app/api/`

## Out of Scope
- Never touch `lib/billing/`
```

---

## 🎓 Inspired By

- **[Peter Steinberger](https://steipete.me)** - "Just Talk To It", shipping at inference-speed
- **[Simon Willison](https://simonwillison.net)** - Vibe engineering, senior practices
- **[Armin Ronacher](https://lucumr.pocoo.org)** - Plan mode is just a prompt

---

## 📈 Stats

```
✅ 32 skills (all stacks)
✅ 3 harnesses unified  
✅ 1 source of truth
✅ 0 orchestrators
✅ 0 charades
```

---

## ✅ Verify Setup

```bash
# Check symlinks exist
ls -la ~/.config/opencode/AGENTS.md
ls -la ~/.codex/AGENTS.md
ls -la ~/.claude/CLAUDE.md

# All should point to ~/work/agent/stacks/*
readlink ~/.config/opencode/AGENTS.md
readlink ~/.codex/AGENTS.md  
readlink ~/.claude/CLAUDE.md

# Skills shared
ls ~/work/agent/skills/
```

---

## 🚀 Next Steps

1. ✅ Test with your primary harness
2. ✅ Add `AGENTS.md` to your projects
3. ✅ Discover and refine patterns as you work
4. ✅ Keep it simple

---

**Just talk to it. Ship fast. Stay in control.**
