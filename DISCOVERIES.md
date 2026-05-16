# Latest Discoveries (May 2026)

## Sources Analyzed
- Simon Willison: "Parallel Agents", "Agentic Loops", "Vibe Engineering"
- Jesse Vincent: "How I'm using coding agents"
- Anthropic: "Claude Code Best Practices"  
- Josh Snyder (Sketch.dev): "7 Prompting Habits"
- Peter Steinberger: Gists (MCP CLI, git rules, worktrees)

## Key Insights

### 1. YOLO Mode = Critical for Productivity
Auto-approve everything, but do it safely:
- Docker containers (restrict files + network)
- GitHub Codespaces (someone else's computer)
- Allowlist network access (prevent exfiltration)

"An AI agent is an LLM wrecking its environment in a loop." - Solomon Hykes

### 2. Parallel Agents (Run 3-8 instances!)
Patterns:
- **Research/PoCs**: "Can library X work?"
- **"How does this work?"**: Explain existing code
- **Small maintenance**: "Fix this deprecation warning"
- **Architect/Implementer**: Separate design from execution
- **Send out a scout**: Learn from agent's mistakes without making them

### 3. Architect/Implementer Pattern (Jesse Vincent)
Two separate sessions:
- **Architect**: Brainstorm → Plan → Review
- **Implementer**: Execute plan in chunks, /clear between each
- Architect resets with double-ESC (no bias)
- Copy reviews between sessions (PM role)

Why: Implementer has clean context, Architect keeps design intent

### 4. Designing Agentic Loops (Simon Willison)
Look for: clear success criteria + trial/error needed
- Debugging (tests pass)
- Performance (benchmark improves)
- Upgrades (tests still pass)
- Container optimization (smaller + tests pass)

### 5. Context Management = CRITICAL
Context window fills fast. Performance degrades.

Strategies:
- `/clear` between unrelated tasks
- `/compact` to summarize (keeps decisions, frees space)
- Subagents for investigation (separate context!)
- `/btw` for quick questions (doesn't enter history)
- After 2 corrections, /clear and restart with better prompt

### 6. "Give Claude a way to verify" = Highest Leverage
Tests, screenshots, expected outputs
Agent can check itself = dramatically better performance

### 7. AGENTS.md / CLAUDE.md Must Be SHORT
If too long, agent ignores it.
Ruthlessly prune. Only include what agent can't infer.

### 8. Git Worktrees for Isolation
```bash
cd .worktrees
git worktree add feature-name
cd feature-name
npm install
claude  # isolated!
```

Run 3-4 parallel features on same repo.

### 9. CLI Tools > MCPs
MCPs pollute context (GitHub MCP = 23k tokens!)
Use: gh, vercel, psql, bun

MCP via CLI (Peter): pnpm mcp:call (progressive disclosure)

### 10. CodeRabbit Review with Role-Play
"Should we hire this reviewer? Which issues to fix?"
Prevents credulous acceptance of bad suggestions.

## What Changed in Our System
- Added parallel agent patterns
- Added YOLO mode safety guidelines
- Added agentic loop design
- Added Architect/Implementer workflow
- Added context management strategies
- Added "send out a scout" pattern
- Emphasized "give agent way to verify" as highest leverage
- Added git worktrees guide
- Added non-interactive mode examples

## Stats
- AGENTS.md: 235 lines → 495 lines (but WAY more practical!)
- Skills: 32 (unchanged)
- Philosophy: Same (Just Talk To It)
- Stacks unified: 3 (opencode, codex, claude)
