---
paths:
  - "scripts/R/**"
  - "scripts/Mplus/**"
  - "writing/**"
---

# Quality Gates & Scoring Rubrics

## Thresholds

- **80/100 = Save** — good enough to commit
- **90/100 = Share** — ready to show advisor or submit
- **95/100 = Excellence** — aspirational

## R Scripts (.R)

| Severity | Issue | Deduction |
|----------|-------|-----------|
| Critical | Syntax errors / won't run | -100 |
| Critical | Wrong reverse coding | -30 |
| Critical | Hardcoded absolute paths | -20 |
| Major | Missing `set.seed()` | -10 |
| Major | Packages not loaded at top | -10 |
| Major | Missing data handling undocumented | -5 |
| Minor | Long lines (>100 chars, non-formula) | -1 per line |

## Mplus Files (.inp)

| Severity | Issue | Deduction |
|----------|-------|-----------|
| Critical | Model won't run / syntax error | -100 |
| Critical | Wrong estimator for data type | -20 |
| Critical | CATEGORICAL not declared for ordinal items | -15 |
| Major | Missing STANDARDIZED in OUTPUT | -5 |
| Major | Missing fit indices reported | -5 |
| Minor | Non-descriptive file name | -2 |

## Academic Writing (manuscripts, COMPS, proposals)

| Severity | Issue | Deduction |
|----------|-------|-----------|
| Critical | Fabricated or unverifiable citations | -30 |
| Critical | Claims not supported by cited evidence | -20 |
| Major | Undefined constructs or abbreviations | -10 |
| Major | Inconsistent terminology across sections | -5 |
| Major | Missing limitations section | -5 |
| Minor | Grammar / typo / APA formatting errors | -2 each |

## Enforcement

- **Score < 80:** Flag blocking issues before proceeding.
- **Score < 90:** Allow but note recommendations.
- User can override with justification.

## Quality Reports

Generated at significant milestones (COMPS submission, paper submission, analysis completion).
Use `templates/quality-report.md` if available.
Save to `quality_reports/`.
