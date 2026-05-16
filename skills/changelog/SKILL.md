---
name: changelog
summary: Create or update CHANGELOG.md following Keep a Changelog format
read_when: User asks to create changelog, update changelog, generate release notes, or prepare version release
triggers:
  - changelog
  - update changelog
  - create changelog
  - generate changelog
  - release notes
  - prepare release
  - version bump
---

# Changelog Generator

Create or update `CHANGELOG.md` following [Keep a Changelog](https://keepachangelog.com/en/1.0.0/) format with automatic commit analysis.

## Purpose

Automate changelog creation by analyzing git commits since last release and categorizing changes into standard sections.

## Workflow

### 1. Analyze Commits

```bash
# Get commits since last tag (or all if no tags)
git log $(git describe --tags --abbrev=0 2>/dev/null || git rev-list --max-parents=0 HEAD)..HEAD --oneline

# Or between specific versions
git log v1.0.0..HEAD --oneline
```

### 2. Categorize by Conventional Commits

Use commit message prefixes to categorize:

| Prefix | Category | Description |
|--------|----------|-------------|
| `feat:` | **Added** | New features |
| `fix:` | **Fixed** | Bug fixes |
| `refactor:` | **Changed** | Code refactoring |
| `docs:` | **Changed** | Documentation updates |
| `chore:` | **Changed** | Maintenance tasks |
| `perf:` | **Changed** | Performance improvements |
| `test:` | **Changed** | Test updates |
| `style:` | **Changed** | Code style changes |
| `ci:` | **Changed** | CI/CD changes |
| `build:` | **Changed** | Build system changes |
| `revert:` | **Fixed** | Reverted changes |
| **BREAKING CHANGE** | **Changed** | Breaking changes (highlight!) |

### 3. Format Structure

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

---

## [Unreleased]

### Added
- New feature X
- New feature Y

### Changed
- Refactored Z for better performance
- Updated documentation for A

### Fixed
- Bug in B that caused C
- Issue with D

### Removed
- Deprecated feature E

## [1.0.0] - 2025-01-29

### Added
- Initial release

---

[Unreleased]: https://github.com/user/repo/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/user/repo/releases/tag/v1.0.0
```

### 4. Update Workflow

**For new version:**
1. Read existing CHANGELOG.md (if exists)
2. Collect commits since last version
3. Categorize by prefix
4. Insert new version section below `[Unreleased]`
5. Update comparison links at bottom
6. Preserve all previous versions

**For unreleased changes:**
1. Add to `[Unreleased]` section
2. Update regularly during development
3. Move to versioned section when releasing

## Best Practices

### Group Related Changes
```markdown
### Added
- **Authentication**: OAuth2 provider, JWT tokens, refresh flow
- **API**: New endpoints for user management, bulk operations
- **UI**: Dashboard redesign, mobile responsive nav
```

### Be Specific
```markdown
❌ "Fixed bugs"
✅ "Fixed memory leak in WebSocket connection handler"

❌ "Updated dependencies"
✅ "Updated React 18 → 19 for improved concurrent rendering"
```

### Highlight Breaking Changes
```markdown
### Changed
- **BREAKING**: Authentication now requires API key in header instead of query param
- **BREAKING**: Removed deprecated `/v1/users` endpoint (use `/v2/users`)
```

### Link to Issues/PRs
```markdown
### Fixed
- Memory leak in connection pool (#123)
- Race condition in cache invalidation (#456)
```

## Special Cases

### Initial Release (v1.0.0)
Keep it simple:
```markdown
## [1.0.0] - 2025-01-29

### Added
- Initial release with core features
- User authentication
- API endpoints
- Documentation
```

### Pre-releases (beta, alpha)
```markdown
## [1.0.0-beta.1] - 2025-01-15

### Added
- Beta feature X (experimental)

### Known Issues
- Performance degradation in Y
- Edge case in Z
```

### Hotfixes
```markdown
## [1.0.1] - 2025-01-30

### Fixed
- Critical security vulnerability in auth (CVE-2025-1234)
- Production crash in payment processing
```

## Automation Tips

### Extract from Commits
```bash
# Get all 'feat:' commits
git log --oneline --grep="^feat:" v1.0.0..HEAD

# Get all 'fix:' commits  
git log --oneline --grep="^fix:" v1.0.0..HEAD

# Check for breaking changes
git log --grep="BREAKING CHANGE" v1.0.0..HEAD
```

### Auto-categorize
1. Parse each commit message
2. Extract prefix (`feat`, `fix`, etc.)
3. Map to changelog category
4. Group by category
5. Format as bullet points

### Date Format
Use ISO date: `YYYY-MM-DD` (e.g., `2025-01-29`)

## Output

### Ask Before Writing
1. Show categorized changes to user
2. Ask for confirmation
3. Request additional context if needed
4. Let user edit/reorder before writing

### Preserve History
- Never delete previous versions
- Always append new sections at top (below Unreleased)
- Keep comparison links updated

### Commit Message
```bash
git commit -m "docs: update CHANGELOG.md for v1.1.0"
```

## Example Invocations

```
"update changelog for v1.1.0"
"create changelog from commits since v1.0.0"
"generate release notes for the new version"
"prepare changelog for release"
```

## Related

- Git log and commit history analysis
- Conventional Commits spec
- Semantic versioning
- Release automation

---

**Remember**: Changelog is for humans, not machines. Focus on what changed and why it matters to users.
