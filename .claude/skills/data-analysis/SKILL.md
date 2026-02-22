---
name: data-analysis
description: End-to-end quantitative analysis workflow — R data preparation and visualization, Mplus model specification, and results interpretation
disable-model-invocation: true
argument-hint: "[dataset path or description of analysis goal, e.g., 'LPA on motivation scales using data/survey.csv']"
allowed-tools: ["Read", "Grep", "Glob", "Write", "Edit", "Bash", "Task"]
---

# Data Analysis Workflow

Run a quantitative analysis: data preparation in R, model specification in Mplus (if SEM/LPA/longitudinal), and interpretation of results.

**Input:** `$ARGUMENTS` — a dataset path and/or a description of the analysis goal.

---

## Constraints

- **Follow R conventions** in `.claude/rules/r-code-conventions.md`
- **Follow Mplus conventions** in `.claude/rules/mplus-conventions.md`
- **Save all R scripts** to `scripts/R/` with descriptive names
- **Save all Mplus .inp files** to `scripts/Mplus/`
- **Save outputs** (figures, tables, RDS) to `data/processed/` or `output/`
- **Run review-r agent** on generated R scripts before presenting results

---

## Workflow Phases

### Phase 1: Data Preparation (R)

1. Read `.claude/rules/r-code-conventions.md`
2. Create R script with header (title, author, purpose, inputs, outputs)
3. Load packages at top (`library()`, never `require()`)
4. Set seed: `set.seed(YYYYMMDD)`
5. Load data and inspect:
   - Variable names, types, distributions
   - Missing data rates (flag if > 5% on key variables)
   - Reverse-coded items (handle before computing composites)
6. Compute scale scores / composites (after checking reliability)
7. Export cleaned dataset as `.csv` and `.dat` (for Mplus)

```r
# Export for Mplus (no variable names, no quotes, missing = 999)
write.table(df_clean, "data/processed/data_for_mplus.dat",
            row.names = FALSE, col.names = FALSE,
            na = "999", sep = " ")
```

### Phase 2: Descriptive Analysis (R or SPSS)

Generate:
- **Summary statistics:** M, SD, min, max, skewness, kurtosis
- **Reliability:** Cronbach's α (or McDonald's ω) per scale
- **Correlations:** correlation matrix with significance
- **Distributions:** histograms or density plots for key variables
- **Group comparisons:** if relevant (gender, grade level, school type)

### Phase 3: Main Analysis

#### For SEM / CFA (Mplus)
1. Read `.claude/rules/mplus-conventions.md`
2. First run a measurement model (CFA) — check fit before structural model
3. Write `.inp` file following the template in conventions
4. Check fit indices: CFI, TLI, RMSEA (90% CI), SRMR
5. If poor fit: examine modification indices (MODINDICES(10) in OUTPUT)
6. Run structural model once measurement model is acceptable

#### For LPA / LCA (Mplus)
1. Run k = 1 through 5 (or 6) class solutions
2. Compare BIC, aBIC, LMR-LRT (TECH11), BLRT (TECH14), entropy
3. Examine profile interpretability — do profiles make theoretical sense?
4. Save final classification: `SAVE = CPROBABILITIES;`
5. Bring class assignments back into R for further analyses

#### For Meta-Analysis (R)
- Use `metafor` package
- Compute or convert effect sizes (r, d, g) as needed
- Report heterogeneity (I², τ²) and moderator analyses if planned

#### For Longitudinal Models (Mplus)
- Growth curve: specify time scores carefully (fix intercept @0)
- CLPM: document autoregressive and cross-lagged paths explicitly
- Test measurement invariance across time before comparing means

### Phase 4: Results Preparation

**Tables (R):**
- Use `flextable` or `knitr::kable` for Word-compatible tables
- Include: M, SD, reliability, correlations OR regression coefficients, SE, p, CI, effect size
- Export as `.docx` using `officer` package, or as `.csv` for manual formatting in Word

**Figures (R):**
- Use `ggplot2` with `theme_research()` from conventions
- Explicit dimensions: `ggsave(width = 6.5, height = 4, dpi = 300)`
- Save as both `.pdf` and `.png`

### Phase 5: Save and Review

1. `saveRDS()` for all key R objects
2. Run the r-reviewer agent: "Review the script at `scripts/R/[script_name].R`"
3. Address any Critical or Major issues

---

## Script Structure (R)

```r
# ============================================================
# [Descriptive Title]
# Author: Siyuan
# Purpose: [What this script does]
# Inputs:  [Data files]
# Outputs: [Tables, figures, RDS files]
# ============================================================

# 0. Setup ----
library(tidyverse)
library(psych)       # reliability, descriptives
library(flextable)   # Word-compatible tables

set.seed(20240901)

dir.create("output", recursive = TRUE, showWarnings = FALSE)

# 1. Data Loading ----

# 2. Data Cleaning & Scoring ----

# 3. Descriptive Analysis ----

# 4. Main Analysis ----

# 5. Export ----
```

---

## Important

- **Check reverse coding first** — wrong direction invalidates all subsequent analyses.
- **Show descriptives before models** — never jump straight to SEM.
- **Report effect sizes** alongside significance tests.
- **Document missing data strategy** — note whether FIML (Mplus), multiple imputation, or listwise was used and why.
- **Use relative paths** — all paths relative to repo root.
