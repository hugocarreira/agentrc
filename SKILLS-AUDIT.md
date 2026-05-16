# Skills Audit Results

**Date:** 2026-05-XX  
**Total Skills:** 32  
**Total Lines:** ~8,185  

---

## TL;DR

**Problems Found:**
- 41% das skills são marketing/CRO (over-indexed!)
- 7 skills são BLOAT puro (~1,605 linhas de conteúdo genérico)
- 4 skills REDUNDANTES (podem ser merged)
- Alguns são só "prompt templates", não skills reais

**Recommendation:**
```
Remove 8 skills bloat → Save ~1,605 lines
Merge 4 redundant    → Save ~596 lines
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
32 skills → 24 skills (27% reduction)
8,185 lines → ~6,000 lines
```

---

## Skills by Quality

### ✅ KEEP (18 skills) - High Quality

**Dev Workflow (5):**
- agent-browser (569 lines) - Browser automation
- commit-and-push (165 lines) - Atomic commits
- pullrequest (35 lines) - GitHub PR creation
- test-and-verify (223 lines) - Tests in same context
- simplify (53 lines) - Code cleanup

**Frontend (7):**
- frontend-design (45 lines) - Design system patterns
- accessibility (442 lines) - WCAG 2.2
- web-design-guidelines (40 lines) - UI review
- vercel-react-view-transitions (321 lines) - React animations
- best-practices (585 lines) - Modern web dev
- security-best-practices (88 lines) - Security audit
- next-best-practices (155 lines) - Next.js patterns

**Next.js (2 more):**
- next-cache-components (413 lines) - Next 16 caching
- next-upgrade (52 lines) - Migration helper

**SEO/Marketing (4):**
- seo (515 lines) - Core SEO
- programmatic-seo (239 lines) - Pages at scale
- competitor-alternatives (257 lines) - Comparison pages
- product-marketing-context (242 lines) - Context doc

**Performance (2):**
- core-web-vitals (443 lines) - LCP/INP/CLS
- performance (362 lines) - General perf

**Utilities (1):**
- find-skills (144 lines) - Skill discovery

---

### ❌ REMOVE (7 skills) - Bloat

1. **premium-saas-design** (573 lines)
   - Problema: Niche demais, workflow específico para "$5k+ SaaS"
   
2. **marketing-psychology** (456 lines)
   - Problema: Genérico, mental models que qualquer um busca no Google
   
3. **seo-audit** (413 lines)
   - Problema: REDUNDANTE com `seo` skill
   
4. **page-cro** (183 lines)
   - Problema: REDUNDANTE com `landing-page`
   
5. **web-quality-audit** (171 lines)
   - Problema: Só aponta para outras skills (wrapper inútil)
   
6. **monetization-strategy** (152 lines)
   - Problema: Generic business strategy, não é skill técnica
   
7. **marketing-ideas** (46 lines)
   - Problema: Só diz "gere 5 ideias" - trivial demais

**Total to remove: ~1,994 lines**

---

### 🔄 MERGE (Optional)

1. Merge `seo-audit` → `seo` (add audit section)
2. Merge `page-cro` → `landing-page` (add CRO tips)
3. Keep `pullrequest` separate (small enough, distinct workflow step)

---

### ⚠️ BORDERLINE (Keep for now, but watch)

1. **product-strategy** (113 lines) - Generic PM framework
2. **landing-page** (110 lines) - Could absorb page-cro content
3. **signup-flow-cro** (360 lines) - Useful but long
4. **onboarding-cro** (221 lines) - Useful but could merge with signup

---

## Categories Breakdown

### Before Cleanup:
```
Dev Workflow:     5 skills (  508 lines)  16%
Frontend:        11 skills (3,188 lines)  39%
SEO/Marketing:   13 skills (3,339 lines)  41%  ← OVER-INDEXED!
Performance:      3 skills (  976 lines)  12%
Utilities:        1 skill  (  144 lines)   2%
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Total:           32 skills (8,185 lines) 100%
```

### After Cleanup (Proposed):
```
Dev Workflow:     5 skills (  508 lines)  25%
Frontend:         7 skills (2,015 lines)  34%
SEO/Marketing:    6 skills (1,253 lines)  21%  ← BALANCED!
Performance:      2 skills (  805 lines)  13%
Utilities:        1 skill  (  144 lines)   2%
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Total:           24 skills (6,000 lines) 100%
```

---

## Recommended Actions

### Step 1: Remove Clear Bloat
```bash
cd ~/work/agent/skills
rm -rf premium-saas-design
rm -rf marketing-psychology
rm -rf marketing-ideas
rm -rf monetization-strategy
rm -rf product-strategy
rm -rf web-quality-audit
```

### Step 2: Merge Redundant
```bash
# Merge seo-audit → seo (add audit section)
# Merge page-cro → landing-page (add CRO section)
# Delete originals
rm -rf seo-audit
rm -rf page-cro
```

### Step 3: Result
```
Before: 32 skills, 8,185 lines
After:  24 skills, ~6,000 lines (27% reduction)
```

---

## Verdict

**Current collection:** Over-indexed on marketing/CRO, has generic business content that doesn't belong.

**After cleanup:** Lean, focused, high-quality set of truly technical skills.

**Action:** Execute cleanup? (removes 8 skills, saves ~2,200 lines of bloat)
