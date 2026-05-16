---
name: ship
summary: Ship changes - auto branch, commit files separately, push, and open PR
read_when: User says "ship", "ship this", "ship it", or wants to commit and create PR in one command
triggers:
  - ship
  - ship this
  - ship it
  - ready to ship
---

# Ship

Complete shipping workflow: branch (if on main), commit each file with context-aware messages, push, and open PR.

## Purpose

Automate the entire shipping flow with intelligent file-by-file commits and automatic PR creation.

## Workflow

### 1. Check Current Branch

```bash
current_branch=$(git branch --show-current)

if [ "$current_branch" = "main" ] || [ "$current_branch" = "master" ]; then
  echo "⚠️  On main branch - will create feature branch"
  need_branch=true
else
  echo "✅ On feature branch: $current_branch"
  need_branch=false
fi
```

### 2. Create Branch (if needed)

**If on main/master:**

Ask user for branch name or auto-generate from changes:
```bash
# Auto-generate from commits or file changes
# Examples:
#   feat/add-authentication
#   fix/memory-leak
#   refactor/api-cleanup
#   docs/update-readme

git checkout -b <branch-name>
```

**Branch naming convention:**
- `feat/` - New features
- `fix/` - Bug fixes
- `refactor/` - Code refactoring
- `docs/` - Documentation
- `chore/` - Maintenance
- `perf/` - Performance improvements

### 3. Analyze Changes

```bash
# Get all changed files
git status --short

# Group by logical context:
# - Related files (e.g., component + test)
# - Separate concerns (e.g., config vs. code)
# - Dependencies (e.g., package.json separate)
```

### 4. Commit Each File/Group Separately

**Smart grouping:**

1. **Related files together:**
   ```bash
   # Component + test
   git add src/components/Button.tsx src/components/Button.test.tsx
   git commit -m "feat: add Button component with tests"
   ```

2. **Config files separate:**
   ```bash
   git add package.json package-lock.json
   git commit -m "chore: update dependencies"
   ```

3. **Documentation separate:**
   ```bash
   git add README.md CHANGELOG.md
   git commit -m "docs: update README and changelog"
   ```

4. **Single purpose commits:**
   ```bash
   git add src/auth/login.ts
   git commit -m "feat: implement OAuth2 login"
   
   git add src/auth/logout.ts
   git commit -m "feat: implement logout functionality"
   ```

### 5. Generate Commit Messages

**Use Conventional Commits:**

```
<type>: <description>

[optional body]

[optional footer]
```

**Types:**
- `feat:` - New feature
- `fix:` - Bug fix
- `refactor:` - Code refactoring
- `docs:` - Documentation
- `chore:` - Maintenance
- `test:` - Tests
- `perf:` - Performance
- `style:` - Code style

**Smart message generation:**
1. Analyze file content/diff
2. Detect intent (add/update/remove)
3. Extract key changes
4. Generate concise message

**Examples:**
```bash
# New file
git add src/hooks/useAuth.ts
# → "feat: add useAuth hook for authentication"

# Modified file
git add src/api/users.ts
# → "fix: handle empty response in users API"

# Deleted file
git rm src/legacy/old-auth.ts
# → "refactor: remove legacy authentication system"

# Multiple related files
git add src/components/{Header,Footer,Layout}.tsx
# → "feat: add layout components (Header, Footer, Layout)"
```

### 6. Review Before Committing

**Show user:**
1. Files to commit
2. Generated commit message
3. Brief diff summary

**Ask for confirmation:**
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📦 Commit #1

Files:
  src/components/Button.tsx
  src/components/Button.test.tsx

Message:
  feat: add Button component with tests

Changes:
  + 45 lines (new component)
  + 23 lines (test suite)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Commit this? (yes/edit/skip)
```

### 7. Push to Remote

```bash
# Push branch (with -u flag if first push)
if ! git rev-parse --abbrev-ref --symbolic-full-name @{u} &>/dev/null; then
  git push -u origin $(git branch --show-current)
else
  git push
fi
```

### 8. Create Pull Request

**Use GitHub CLI:**

```bash
# Get branch name and commit messages
branch=$(git branch --show-current)
base_branch="main"  # or "master"

# Get all commits in this branch (not in base)
commits=$(git log $base_branch..HEAD --oneline)

# Generate PR title from branch name or first commit
# feat/add-auth → "Add authentication"
# fix/memory-leak → "Fix memory leak"

# Generate PR body from all commits
pr_body=$(cat <<EOF
## Summary

[Auto-generated from commits]

## Commits

$commits

## Changes

- Added: [list new features]
- Fixed: [list bug fixes]
- Changed: [list refactoring]
EOF
)

# Create PR
gh pr create \
  --title "$pr_title" \
  --body "$pr_body" \
  --base $base_branch \
  --head $branch
```

### 9. Output PR URL

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✅ Shipped!

Branch:  feat/add-authentication
Commits: 3
PR:      https://github.com/user/repo/pull/123

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

## Advanced Options

### Skip PR Creation

```bash
# Just commit + push (no PR)
"ship this without PR"
```

### Custom Branch Name

```bash
# User specifies branch
"ship this on branch feat/new-feature"
```

### Custom Commit Grouping

```bash
# User specifies how to group
"ship this, commit each file separately"
"ship this, group by directory"
"ship this, one commit for everything"
```

### Amend Last Commit

```bash
# If just pushed and want to add more
"ship this, amend last commit"
```

## Best Practices

### Commit Granularity

**Good:**
```
✅ feat: add user authentication
✅ test: add auth tests
✅ docs: update auth documentation
```

**Bad:**
```
❌ chore: updates
❌ fix: stuff
❌ WIP
```

### File Grouping Logic

1. **Component + Test** → Same commit
2. **Config files** → Separate commit
3. **Dependencies** → Separate commit (package.json)
4. **Documentation** → Separate commit
5. **Unrelated features** → Separate commits
6. **Bug fixes** → Separate from features

### Branch Protection

**Never force push to:**
- `main`
- `master`
- `production`
- `develop`

**Warn if:**
- Commits already pushed (risk of rewrite)
- Branch shared with others

## Error Handling

### Uncommitted Changes Conflict

```bash
# If files have merge conflicts or errors
echo "❌ Cannot commit - resolve conflicts first"
exit 1
```

### Push Rejected

```bash
# If push fails (e.g., branch protection)
echo "❌ Push rejected - check branch protection rules"
echo "Try: git pull --rebase origin $(git branch --show-current)"
```

### PR Already Exists

```bash
# If PR already exists for this branch
echo "⚠️  PR already exists: [URL]"
echo "Update existing PR instead? (yes/no)"
```

## Integration with Existing Skills

This skill combines:
- **commit-and-push** - Atomic commits + push
- **pullrequest** - PR creation with gh CLI

**Key differences:**
- Automatic branching (if on main)
- Smart file-by-file commits (not single commit)
- Auto-generated commit messages
- Single command for entire flow

## Example Invocations

**Simple:**
```
"ship"
"ship this"
"ship it"
```

**With options:**
```
"ship this on branch feat/new-feature"
"ship this, commit each file separately"
"ship without PR"
"ship and skip docs"
```

**After changes:**
```
User makes changes to 5 files

User: "ship"

Agent:
1. Detects on main → creates feat/add-oauth branch
2. Groups files:
   - src/auth/oauth.ts + test → commit 1
   - config/auth.json → commit 2
   - README.md → commit 3
3. Pushes branch
4. Creates PR with summary
5. Returns PR URL
```

## Related

- **commit-and-push** - Manual commit workflow
- **pullrequest** - Manual PR creation
- Git best practices
- Conventional Commits

---

**Remember**: This automates the full flow, but you can still use individual skills (commit-and-push, pullrequest) for more control.
