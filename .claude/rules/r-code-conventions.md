---
paths:
  - "scripts/R/**"
---

# R Code Standards

**Standard:** Reproducible, well-documented research-grade R code.

---

## 1. Reproducibility

- `set.seed()` called ONCE at top (use YYYYMMDD format, e.g., `set.seed(20240901)`)
- All packages loaded at top via `library()` (not `require()`)
- All paths relative to repository root
- `dir.create(..., recursive = TRUE, showWarnings = FALSE)` for output directories

## 2. Function Design

- `snake_case` naming, verb-noun pattern (e.g., `compute_reliability`, `plot_profiles`)
- Brief comment explaining purpose for non-obvious functions
- Default parameters, no magic numbers
- Named return values (lists or tibbles)

## 3. Domain Correctness

- Match scale scoring direction (reverse-coded items handled correctly)
- Check reliability (α or ω) before using composite scores
- Verify missing data treatment matches Mplus (FIML vs listwise vs pairwise)
- For meta-analysis: verify effect size transformations (r → z, d → r)

## 4. Figure Standards

```r
# Suggested palette for educational psychology research
primary_color  <- "#2E4A7A"   # Dark blue
secondary_color <- "#E07B3B"  # Orange
neutral_gray   <- "#6B6B6B"   # Gray

theme_research <- function(base_size = 12) {
  theme_minimal(base_size = base_size) +
    theme(
      plot.title = element_text(face = "bold"),
      legend.position = "bottom",
      panel.grid.minor = element_blank()
    )
}
```

Figure dimensions for manuscripts (adjust as needed):
```r
ggsave(filepath, width = 6.5, height = 4, dpi = 300)  # journal column width
```

## 5. Data Export Pattern

Save computed objects as RDS — avoid re-running slow computations:

```r
saveRDS(result, file.path("data", "processed", "model_output.rds"))
```

## 6. Common Pitfalls

| Pitfall | Impact | Prevention |
|---------|--------|------------|
| Hardcoded absolute paths | Breaks on other machines | Use relative paths |
| Missing `set.seed()` | Non-reproducible results | Set once at top |
| Listwise deletion (unexpected) | Biased estimates | Check `na.action` in each function |
| Wrong reverse coding | Invalid scale scores | Verify with codebook before scoring |
| Conflicting package functions | Silent errors | Use `package::function()` for ambiguous names |

## 7. Line Length

Keep lines ≤ 100 characters. Exception: formula code where breaking harms readability — add a comment explaining the formula.

## 8. Code Quality Checklist

```
[ ] Packages at top via library()
[ ] set.seed() once at top
[ ] All paths relative to repo root
[ ] Output directories created with dir.create()
[ ] Figures: explicit dimensions, 300 dpi for manuscript
[ ] Computed objects saved as RDS
[ ] Reverse coding verified
[ ] Comments explain WHY not WHAT
```
