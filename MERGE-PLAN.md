# Merge Plan - Extract Before Delete

**Goal:** Save 1,285 lines of valuable content from 8 "bloat" skills before deletion.

---

## Summary

| Skill | Lines | Valuable | Action |
|-------|-------|----------|--------|
| premium-saas-design | 573 | 350 (61%) | Merge → frontend-design |
| marketing-psychology | 456 | 400 (88%) | Move → _references/ |
| seo-audit | 413 | 250 (61%) | Merge → seo |
| page-cro | 183 | 100 (55%) | Merge → landing-page + _references/ |
| web-quality-audit | 171 | 70 (41%) | Merge → core-web-vitals |
| monetization-strategy | 152 | 50 (33%) | Move → _references/ |
| product-strategy | 113 | 65 (58%) | Move → _references/ |
| marketing-ideas | 46 | 0 (0%) | DELETE (pure bloat) |
| **TOTAL** | **2,107** | **1,285 (61%)** | |

---

## Phase 1: Create _references/ Structure

```bash
mkdir -p ~/work/agent/skills/_references
```

Purpose: Knowledge base docs (not task-oriented skills)

---

## Phase 2: Extract to References (5 docs)

### 1. marketing-psychology → _references/marketing-psychology-models.md
**Content:** 50+ mental models with examples (lines 27-437)
**Value:** 88% - comprehensive reference
**Size:** ~400 lines
**Used by:** landing-page, page optimization tasks

### 2. page-cro/references/experiments.md → _references/cro-experiments.md
**Content:** Comprehensive CRO experiment library
**Value:** HIGH - specific hypotheses by page type
**Size:** 248 lines
**Used by:** landing-page, frontend-design

### 3. seo-audit/references/ai-writing-detection.md → _references/ai-writing-detection.md
**Content:** AI writing patterns to avoid
**Value:** HIGH - specific and useful
**Size:** 200 lines
**Used by:** seo, content writing

### 4. monetization-strategy → _references/monetization-models.md
**Content:** 7 models with fit/risks/experiments (lines 73-116)
**Value:** MEDIUM - useful framework
**Size:** ~50 lines
**Used by:** product strategy discussions

### 5. product-strategy → _references/product-strategy-canvas.md
**Content:** 9-section canvas with guiding questions (lines 26-88)
**Value:** MEDIUM - legitimate framework
**Size:** ~65 lines
**Used by:** product planning

---

## Phase 3: Merge into Existing Skills

### 3.1 frontend-design ← premium-saas-design

**Extract from premium-saas-design:**

#### Add Section: "The 7 Context Artifacts for Premium Design"
- Lines 29-398 (entire framework)
- Project Brief template
- Content Files structure
- General Vibe Mood Board
- Section-Specific Mood Boards
- Style Guide template
- PRD structure
- Tasks Document

#### Add Section: "Component Resources"
- Lines 400-427
- shadcn/ui (lines 404-407)
- 21st.dev (lines 409-417)
- Three.js (lines 419-422)
- Sketchfab (lines 424-427)

#### Add Section: "Best Practices"
- Lines 429-476
- Section isolation strategy (432-437)
- Screenshot-to-iteration workflow (439-449)
- Auto-update style guide (451-457)

#### Add: "Prompt Templates"
- Lines 491-558
- Generate Style Guide
- Generate PRD
- Build a Section

**Delete from premium-saas-design:** Lines 1-28, 477-488, 560-573 (intro/fluff)

---

### 3.2 landing-page ← page-cro

**Extract from page-cro:**

#### Add Section: "CRO Analysis Framework"
- Lines 26-105
- Value Proposition Clarity (30-41)
- Headline patterns (42-53)
- CTA hierarchy (54-66)
- Social proof patterns (68-77)
- Urgency/scarcity (79-89)
- Friction reduction (91-105)

#### Add Section: "Page-Specific CRO Frameworks"
- Lines 126-151
- Homepage
- Landing Page
- Pricing
- Feature
- Blog

#### Add Reference Link
```markdown
For comprehensive experiment ideas, see: @_references/cro-experiments.md
```

**Delete from page-cro:** Lines 1-24, 155-183 (intro/generic)

---

### 3.3 seo ← seo-audit

**Extract from seo-audit:**

#### Add WARNING Section (top of technical section)
```markdown
## ⚠️ Schema Markup Detection Limitation

**`web_fetch` and `curl` cannot reliably detect structured data.**

Many CMS plugins inject JSON-LD via client-side JavaScript.

**Accurate detection methods:**
1. Browser: `document.querySelectorAll('script[type="application/ld+json"]')`
2. Google Rich Results Test
3. Screaming Frog (renders JS)
```
(Lines 39-51)

#### Add Section: "Technical SEO Checklist"
- Lines 61-156
- Crawlability detailed checks
- URL structure guidelines
- robots.txt rules
- Sitemap best practices

#### Add Section: "On-Page Audit Specifics"
- Lines 159-261
- Title tag specs (50-60 chars, no brand first)
- Meta description (150-160 chars)
- Heading structure rules
- Image optimization

#### Add Section: "Common Issues by Site Type"
- Lines 306-335
- SaaS/Product
- E-commerce
- Content/Blog
- Local Business

#### Add Reference Link
```markdown
For AI writing detection patterns, see: @_references/ai-writing-detection.md
```

**Delete from seo-audit:** Lines 1-37, 336-413 (intro/generic tools)

---

### 3.4 core-web-vitals ← web-quality-audit

**Extract from web-quality-audit:**

#### Add: "Core Web Vitals Targets"
```markdown
## Performance Targets

- **LCP (Largest Contentful Paint):** < 2.5s (good), 2.5-4s (needs improvement), > 4s (poor)
- **INP (Interaction to Next Paint):** < 200ms (good), 200-500ms (needs improvement), > 500ms (poor)
- **CLS (Cumulative Layout Shift):** < 0.1 (good), 0.1-0.25 (needs improvement), > 0.25 (poor)
```
(Lines 25-29)

#### Add Section: "Accessibility Quick Checks"
- Lines 43-67
- Color contrast (4.5:1 text, 3:1 UI)
- Keyboard navigation
- ARIA labels
- Semantic HTML

#### Add Section: "Issue Severity Framework"
```markdown
## Severity Levels

| Severity | Impact | Action |
|----------|--------|--------|
| Critical | Blocking user actions | Fix immediately |
| High | Poor UX, conversion loss | Fix this sprint |
| Medium | Suboptimal experience | Backlog |
| Low | Nice-to-have | Optional |
```
(Lines 107-114)

#### Add Section: "Audit Cadence Checklist"
- Lines 143-162
- Before deploy: Core Web Vitals, A11y, SEO basics
- Weekly: Performance regression
- Monthly: Full audit

**Delete from web-quality-audit:** Lines 1-22, 89-106, 164-171

---

## Phase 4: Delete Skills

After extraction is complete and verified:

```bash
cd ~/work/agent/skills
rm -rf premium-saas-design
rm -rf marketing-psychology
rm -rf seo-audit
rm -rf page-cro
rm -rf web-quality-audit
rm -rf monetization-strategy
rm -rf product-strategy
rm -rf marketing-ideas
```

---

## Phase 5: Update Cross-References

Search and replace in all remaining skills:

```bash
# Find references to deleted skills
rg "@marketing-psychology" --type md
rg "@page-cro" --type md
rg "@seo-audit" --type md

# Update to new references
@marketing-psychology → @_references/marketing-psychology-models.md
@page-cro → @landing-page or @_references/cro-experiments.md
@seo-audit → @seo
```

---

## Expected Results

**Before:**
- 32 skills
- 8,185 total lines
- 8 bloat skills (2,107 lines)

**After:**
- 24 skills
- ~7,363 lines (after merge)
- 5 reference docs (~1,013 lines)
- 0 bloat

**Net change:**
- Skills: 32 → 24 (25% reduction)
- Bloat removed: ~822 lines of generic content
- Value preserved: 1,285 lines merged/moved

---

## Priority Order

1. **HIGH** (do first):
   - Extract premium-saas-design → frontend-design (most valuable)
   - Move page-cro/experiments → _references/
   - Move seo-audit/ai-writing → _references/
   - DELETE marketing-ideas (zero value)

2. **MEDIUM**:
   - Move marketing-psychology → _references/
   - Merge seo-audit → seo
   - Merge page-cro → landing-page

3. **LOW**:
   - Merge web-quality-audit → core-web-vitals
   - Move monetization-strategy → _references/
   - Move product-strategy → _references/
   - Update cross-references

---

## Validation Checklist

After each extraction:
- [ ] New content added to target skill
- [ ] Content makes sense in new context
- [ ] No broken @references
- [ ] Original skill can be deleted
- [ ] Git commit with clear message

---

**Ready to execute?** Start with Phase 1 (create _references/) and work through in priority order.
