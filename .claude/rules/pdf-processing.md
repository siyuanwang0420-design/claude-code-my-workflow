---
paths:
  - "literature/**"
---

# Robust PDF Processing

Use this protocol when reading papers uploaded to `literature/`.

## The Safe Processing Workflow

**Step 1: Receive PDF**
- User uploads PDF to `literature/` or a subfolder
- Claude does NOT attempt to read it directly without checking size first

**Step 2: Check PDF Size**
```bash
pdfinfo paper_name.pdf | grep "Pages:"
ls -lh paper_name.pdf
```

**Step 3: For Long PDFs (> 10 pages), Split and Process in Chunks**
```bash
mkdir -p literature/[paper_name]/

for i in {0..9}; do
  start=$((i*5 + 1))
  end=$(((i+1)*5))
  gs -sDEVICE=pdfwrite -dNOPAUSE -dBATCH -dSAFER \
     -dFirstPage=$start -dLastPage=$end \
     -sOutputFile="literature/[paper_name]/chunk_p$(printf '%03d' $start)-$(printf '%03d' $end).pdf" \
     literature/[paper_name].pdf 2>/dev/null
done
```

**Step 4: Process Chunks One at a Time**
- Read chunks ONE AT A TIME using the Read tool
- Extract key information from each chunk
- Build understanding progressively

**Step 5: Selective Deep Reading**
- After scanning all chunks, identify the most relevant sections
- Read those in detail
- Skip supplementary materials unless needed

## After Reading: Save Notes

Save reading notes to `literature/notes/[Author_Year_ShortTitle].md` using this structure:

```markdown
# [Full Citation]

**Date read:** [YYYY-MM-DD]
**Relevance:** [High / Medium / Low] — [Why relevant to your work]

## Core Argument
[1-2 sentences]

## Theoretical Framework
[Framework(s) used]

## Methods
- **Sample:** [N, population]
- **Design:** [Cross-sectional / Longitudinal / Meta-analysis]
- **Analysis:** [SEM / LPA / MLM / etc.]
- **Key measures:** [Instruments used]

## Key Findings
- [Finding 1]
- [Finding 2]

## Relevance to My Work
[How this relates to your RQs, theory, or methods]

## Gaps / Limitations
[What they acknowledge or you notice]

## BibTeX
```bibtex
@article{...}
```
```

## Error Handling

**If a chunk fails:**
1. Note the chunk (e.g., "p021-025 failed")
2. Try 1-2 page pieces instead
3. If still failing, skip and document the gap

**If Ghostscript not available:**
```bash
pdftk paper.pdf burst output paper_%03d.pdf
```
