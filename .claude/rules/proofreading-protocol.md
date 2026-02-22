---
paths:
  - "writing/**"
  - "quality_reports/**"
---

# Proofreading Protocol

**CRITICAL RULE: Never apply changes directly. Propose all changes first; only apply after explicit user approval.**

## What to Check

1. **Grammar** — subject-verb agreement, article usage, prepositions
2. **Typos** — misspellings, duplicated words, autocorrect errors
3. **APA Style** — citation format, heading levels, numbers, abbreviations, statistics reporting
4. **Consistency** — construct names, abbreviations, tense throughout
5. **Academic quality** — informal language, vague claims, missing hedges ("may suggest" vs "proves")
6. **Argument flow** — does each paragraph connect logically to the next?

## Three-Phase Workflow

### Phase 1: Review & Propose (NO EDITS)

1. Read the entire document
2. Produce a **report** with every proposed change:
   - Location (section + paragraph, or line number if .md)
   - Current text (exact quote)
   - Proposed fix
   - Category (grammar / typo / APA / consistency / clarity)
3. Save report to `quality_reports/proofread_[filename].md`
4. **Do NOT modify any source files**

### Phase 2: User Review

User reviews proposed changes:
- Accepts all, accepts selectively, or requests modifications
- **Only after explicit approval** does the agent proceed

### Phase 3: Apply Fixes

Apply only approved changes:
- Use Edit tool with exact text matches
- Report completion summary

## APA Quick Reference

- **Statistics:** *M* = 3.45, *SD* = 0.78, *r* = .45, *p* = .032, 95% CI [.21, .67]
- **Numbers:** Spell out one through nine; use numerals for 10+
  - Exception: always use numerals before units (3 items, 5 factors)
- **Abbreviations:** Define on first use; use abbreviation consistently after
- **Headings:** Level 1 = Centered Bold; Level 2 = Left-aligned Bold; Level 3 = Indented Bold Italic
- **Citations:** (Author, Year) in text; do not use "et al." for first citation of ≤5 authors
