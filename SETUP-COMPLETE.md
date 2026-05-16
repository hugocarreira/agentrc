# ✅ Setup Complete - Centralized AI Agent Configuration

## 🎉 What Was Done

All AI coding harnesses now share a **single source of truth** at `~/work/agent`

### Before
```
~/.config/opencode/
  ├── AGENTS.md (different)
  ├── agents/ (only here)
  └── skills/ (symlinks to ~/.agents)

~/.codex/
  ├── AGENTS.md (different)
  ├── RTK.md
  └── skills/ (minimal)

~/.claude/
  ├── CLAUDE.md (different)
  ├── RTK.md (different)
  └── skills/ (symlinked to opencode)
```

### After
```
~/work/agent/                    ← SINGLE SOURCE OF TRUTH
  ├── AGENTS-GLOBAL.md           ← Orchestrator rules
  ├── RTK.md                     ← Token optimization
  ├── agents/                    ← 10 specialized agents
  ├── skills/                    ← 32 shared skills
  ├── plugins/                   ← RTK plugin
  └── stacks/
      ├── opencode/AGENTS.md     → symlinked from ~/.config/opencode/
      ├── codex/AGENTS.md        → symlinked from ~/.codex/
      └── claude/CLAUDE.md       → symlinked from ~/.claude/

All configs, skills, and agents now centralized!
```

---

## 🔗 Active Symlinks

### OpenCode
```bash
~/.config/opencode/AGENTS.md → ~/work/agent/stacks/opencode/AGENTS.md
~/.config/opencode/agents    → ~/work/agent/agents/
~/.config/opencode/skills    → ~/work/agent/skills/
~/.config/opencode/plugins   → ~/work/agent/plugins/
```

### Codex
```bash
~/.codex/AGENTS.md → ~/work/agent/stacks/codex/AGENTS.md
~/.codex/RTK.md    → ~/work/agent/RTK.md
~/.codex/skills    → ~/work/agent/skills/
```

### Claude Code
```bash
~/.claude/CLAUDE.md → ~/work/agent/stacks/claude/CLAUDE.md
~/.claude/AGENTS.md → ~/work/agent/stacks/claude/CLAUDE.md
~/.claude/RTK.md    → ~/work/agent/RTK.md
~/.claude/skills    → ~/work/agent/skills/
```

---

## 📊 What's Centralized

### 🤖 10 Specialized Agents
```
~/work/agent/agents/
├── orchestrator.md          ← Brain of the system
├── frontend-developer.md    ← React/Next.js/TypeScript
├── backend-developer.md     ← APIs/databases/auth
├── designer-ui-ux.md        ← UI/UX/design systems
├── devops-engineer.md       ← CI/CD/Docker/K8s
├── product-manager.md       ← PRDs/roadmaps
├── marketing-growth.md      ← SEO/content/CRO
├── code-reviewer.md         ← Quality gate (read-only)
├── security-auditor.md      ← Security audit (read-only)
└── technical-writer.md      ← Docs/changelogs/ADRs
```

### 🛠️ 32 Shared Skills
All harnesses can now use:

**Development**
- `commit-and-push`, `pullrequest`, `test-and-verify`
- `frontend-design`, `best-practices`, `security-best-practices`

**AI/Browser**
- `agent-browser`, `simplify`

**Next.js**
- `next-best-practices`, `next-cache-components`, `next-upgrade`

**SEO/Marketing**
- `seo`, `seo-audit`, `programmatic-seo`
- `marketing-ideas`, `marketing-psychology`

**CRO/Product**
- `page-cro`, `signup-flow-cro`, `onboarding-cro`
- `product-strategy`, `product-marketing-context`

**Design/Performance**
- `premium-saas-design`, `web-design-guidelines`
- `accessibility`, `core-web-vitals`, `performance`

**And more...**
- `competitor-alternatives`, `landing-page`, `monetization-strategy`
- `find-skills`, `web-quality-audit`, `vercel-react-view-transitions`

---

## 🎯 How Each Stack Uses It

### OpenCode (Orchestrator-First)
```markdown
User Request
     ↓
Orchestrator (reads AGENTS-GLOBAL.md)
     ↓
Delegates to specialized agents
     ↓
Quality gates (code-reviewer, security-auditor)
     ↓
Synthesized result back to user
```

### Codex (Peter Steinberger Workflow)
```markdown
User: [short prompt + screenshot]
     ↓
Codex reads stacks/codex/AGENTS.md
     ↓ (includes RTK.md)
Just Talk To It approach
     ↓
One-shot implementation
     ↓
Test in same context
```

### Claude Code (Conversational)
```markdown
User: [natural language request]
     ↓
Claude reads stacks/claude/CLAUDE.md
     ↓ (includes RTK.md)
Iterate fast approach
     ↓
Queue continue messages
     ↓
Atomic commits
```

---

## 💡 Quick Usage Examples

### Update Global Rules (Applies to All)
```bash
cd ~/work/agent
nano AGENTS-GLOBAL.md
git commit -am "refactor: update orchestrator delegation rules"
```
✅ OpenCode, Codex, and Claude all see the change

### Add New Skill (Available to All)
```bash
cd ~/work/agent/skills
mkdir my-workflow
cat > my-workflow/SKILL.md <<'EOF'
---
name: "my-workflow"
description: "Short trigger"
---
# My Workflow
[content]
EOF
```
✅ All three harnesses discover it automatically

### Stack-Specific Tweak
```bash
# Only affects Codex
nano ~/work/agent/stacks/codex/AGENTS.md

# Only affects Claude
nano ~/work/agent/stacks/claude/CLAUDE.md

# Only affects OpenCode
nano ~/work/agent/stacks/opencode/AGENTS.md
```

### Update RTK Config (Codex + Claude)
```bash
nano ~/work/agent/RTK.md
```
✅ Both Codex and Claude see it (OpenCode uses AGENTS-GLOBAL.md)

---

## 🔍 Verify Everything Works

### Test OpenCode
```bash
# Should show your centralized config
cat ~/.config/opencode/AGENTS.md

# Skills should be accessible
ls ~/.config/opencode/skills/

# Agents should be there
ls ~/.config/opencode/agents/
```

### Test Codex
```bash
# Should include RTK.md
cat ~/.codex/AGENTS.md

# Skills centralized
ls ~/.codex/skills/
```

### Test Claude Code
```bash
# Should reference RTK.md
cat ~/.claude/CLAUDE.md

# Same skills as others
ls ~/.claude/skills/
```

---

## 📝 Maintenance

### Re-run Setup (Safe)
```bash
cd ~/work/agent
./setup-symlinks.sh
```
- Auto-backs up existing files
- Recreates all symlinks
- Safe to run multiple times

### Check Symlink Health
```bash
# All should point to ~/work/agent
ls -la ~/.config/opencode/AGENTS.md
ls -la ~/.codex/AGENTS.md
ls -la ~/.claude/CLAUDE.md
```

### Restore from Backup (If Needed)
```bash
# Backups are timestamped
ls -la ~/.config/opencode/*.backup.*
ls -la ~/.codex/*.backup.*
ls -la ~/.claude/*.backup.*
```

---

## 🎓 Best Practices

### Edit in Central Location
```bash
# ✅ CORRECT - Edit source
nano ~/work/agent/AGENTS-GLOBAL.md

# ❌ WRONG - Don't edit symlink targets
nano ~/.config/opencode/AGENTS.md  # This works but confusing
```

### Commit Changes
```bash
cd ~/work/agent
git add .
git commit -m "feat: add new skill X"
git push  # If you have a remote
```

### Project-Specific Configs
```bash
cd ~/work/my-project

# Reference global, add project-specific
cat > AGENTS.md <<'EOF'
READ ~/work/agent/AGENTS-GLOBAL.md BEFORE ANYTHING.

# My Project Rules
[specific conventions]
EOF
```

---

## 🚀 Next Steps

1. ✅ **Test with your primary harness**
   ```bash
   # OpenCode, Codex, or Claude - all should work
   ```

2. ✅ **Customize stack configs if needed**
   ```bash
   nano ~/work/agent/stacks/{opencode,codex,claude}/*.md
   ```

3. ✅ **Add project-specific AGENTS.md files**
   ```bash
   # In each project
   echo 'READ ~/work/agent/AGENTS-GLOBAL.md BEFORE ANYTHING.' > AGENTS.md
   ```

4. ✅ **Discover and add new patterns**
   ```bash
   # As you find useful workflows
   cd ~/work/agent
   # Document in AGENTS-GLOBAL.md or create new skill
   ```

---

## 📚 Documentation

- **README.md** - Full system overview
- **AGENTS-GLOBAL.md** - Orchestrator rules (OpenCode)
- **RTK.md** - Token optimization (Codex + Claude)
- **AGENTS.template.md** - Template for new projects
- **docs/shipping-checklist.md** - Deployment guide
- **docs/refactoring-guide.md** - Code quality guide

---

## 🎉 Success!

You now have a **single source of truth** for all AI coding configurations.

- ✅ No more duplicate configs
- ✅ No more sync issues
- ✅ Update once, applies everywhere
- ✅ 32 skills accessible to all harnesses
- ✅ 10 specialized agents for orchestrated work
- ✅ Stack-specific behaviors preserved

**Happy shipping at inference-speed! 🚀**
