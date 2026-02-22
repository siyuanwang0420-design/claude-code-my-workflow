---
name: review-paper
description: Critical review of academic manuscripts in educational psychology — argument structure, measurement quality, analytical approach, theoretical grounding, and potential reviewer objections
disable-model-invocation: true
argument-hint: "[paper filename in literature/ or path to .pdf]"
allowed-tools: ["Read", "Grep", "Glob", "Write", "Task"]
---

# Manuscript Review

Produce a thorough, constructive review of an academic manuscript — the kind of report a top journal referee in educational psychology would write.

**Input:** `$ARGUMENTS` — path to a paper (.pdf or .txt), or a filename in `literature/`.

---

## Steps

1. **Locate and read the manuscript.** Check:
   - Direct path from `$ARGUMENTS`
   - `literature/$ARGUMENTS`
   - Glob for partial matches

2. **Read the full paper** end-to-end. For long PDFs, read 5 pages at a time.

3. **Evaluate across 6 dimensions** (see below).

4. **Generate 3-5 "reviewer objections"** — the tough questions a top referee would ask.

5. **Produce the review report.**

6. **Save to** `quality_reports/paper_review_[sanitized_name].md`

---

## Review Dimensions

### 1. Argument Structure & Theoretical Grounding
- Is the research question clearly stated and theoretically motivated?
- Which theoretical framework(s) anchor the study? Are they applied correctly?
- Is the logical flow sound (theory → hypotheses → design → results → interpretation)?
- Do the conclusions match the findings (no overclaiming)?
- Are limitations acknowledged honestly?

### 2. Measurement & Construct Validity
- How are key constructs operationalized? Is the measurement defensible?
- Are scales used as intended (same sample type, age group, cultural context)?
- Is reliability (α, ω) reported and adequate?
- Are CFA/measurement models tested before SEM? Do fit indices meet standards?
- Are validity claims (convergent, discriminant, factorial) supported?

### 3. Research Design & Analytical Approach
- Is the design appropriate for the research question (cross-sectional vs. longitudinal)?
- What statistical method is used? Is it appropriate?
- Is missing data handled properly (FIML, multiple imputation)?
- Are control variables theoretically justified?
- Are effect sizes reported and interpreted (not just p-values)?
- Are assumptions checked (normality, invariance, etc.)?

### 4. Literature Positioning
- Are the key theoretical and empirical papers cited?
- Is prior work characterized accurately (no misrepresentation)?
- Is the contribution clearly differentiated from existing work?
- Are there missing citations a reviewer would flag?

### 5. Writing Quality
- Clarity and precision of language
- Consistent use of construct terminology throughout
- Abstract effectively summarizes RQ, method, and findings
- APA formatting applied correctly
- Tables and figures are self-contained (titles, notes, units)

### 6. Presentation
- Are tables and figures well-designed and appropriately complex?
- Is the paper the right length for its contribution?
- Any typos, grammatical errors, or formatting inconsistencies?

---

## Output Format

```markdown
# Manuscript Review: [Paper Title]

**Date:** [YYYY-MM-DD]
**File:** [path]
**Journal target (if known):** [Journal name]

## Summary Assessment

**Overall recommendation:** [Strong Accept / Accept / Revise & Resubmit / Reject]

[2-3 paragraph summary: main contribution, strengths, and key concerns]

## Strengths

1. [Strength 1]
2. [Strength 2]
3. [Strength 3]

## Major Concerns

### MC1: [Title]
- **Dimension:** [Argument / Measurement / Design / Literature / Writing / Presentation]
- **Issue:** [Specific description]
- **Suggestion:** [How to address it]
- **Location:** [Section / page / table if applicable]

[Repeat for each major concern]

## Minor Concerns

### mc1: [Title]
- **Issue:** [Description]
- **Suggestion:** [Fix]

## Reviewer Objections

The tough questions a top referee would likely raise:

### RO1: [Question]
**Why it matters:** [Why this could be fatal]
**How to address it:** [Suggested response or additional analysis]

[Repeat for 3-5 objections]

## Summary Ratings

| Dimension | Rating (1–5) |
|-----------|-------------|
| Argument & Theory | [N] |
| Measurement & Validity | [N] |
| Design & Analysis | [N] |
| Literature | [N] |
| Writing | [N] |
| Presentation | [N] |
| **Overall** | **[N]** |
```

---

## Principles

- **Be constructive.** Every criticism should come with a suggestion.
- **Be specific.** Reference exact sections, page numbers, tables.
- **Think like a reviewer at a top ed psych journal** (JEDP, CEP, CPER, JEP, etc.).
- **Distinguish fatal flaws from minor issues.**
- **Acknowledge what's done well.**
- **Do NOT fabricate details.** If you can't read a section clearly, say so.
