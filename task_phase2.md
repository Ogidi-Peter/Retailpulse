# Phase 2 — Exploratory Data Analysis & Visualization

**New skill unlocked:** matplotlib + seaborn
**Combined with:** everything from Phase 1 (pandas groupby, datetime handling, git)

Read `phase2_visualization_guide.pdf` first — it has the concepts and code
patterns you'll need, written specifically against your column names. This
brief is the actual assignment.

## Setup
```bash
pip install matplotlib seaborn
mkdir -p notebooks/reports    # this is where chart images will get saved
```
Start a new notebook: `notebooks/02_eda_visualization.ipynb`. Load
`data/processed/sales_clean.csv` — not the raw file. Phase 1's cleaned
output is the foundation for everything from here on.

## The business questions

You're not just making charts for practice — leadership actually wants
answers to these five questions. Each one maps to a chart type from the
guide. For every chart:
1. Build it
2. Save it to `notebooks/reports/` as a `.png`
3. Write 2-3 sentences underneath it in the notebook (markdown cell)
   answering the actual question — not just describing the chart, but
   what it *means* for the business

### 1. Is revenue growing over time, and is it seasonal?
Build a monthly revenue line chart across the full 2023-2024 range.
Look for: overall trend, and whether specific months spike (hint: think
about what real retail seasonality looks like — December, back-to-school,
etc.)

### 2. Which store is the strongest performer, and which is weakest?
Compare total revenue by store. Then go one level deeper: is a store
"weak" because of fewer transactions, or lower prices, or something else?
Use a second chart or a groupby to support your answer.

### 3. Which product category should the business invest more in?
Compare revenue by category. Also look at *volume* (quantity sold) by
category, not just revenue — a category could have high revenue from a few
expensive items or from many cheap ones, and that distinction matters for
business strategy.

### 4. Are there pricing outliers we should double check?
Boxplot of `unit_price` by `category`. This doubles as your Phase 1
quality check — if your outlier cleaning was correct, you shouldn't see
extreme dots way outside the whiskers anymore. If you do, that's useful
information — go back and check what happened.

### 5. Does weekend shopping behavior differ from weekday?
Compare weekday vs weekend revenue and/or transaction volume. State
whether the effect you find is large enough to matter for staffing or
inventory decisions, or negligible.

## What "done" looks like

- A notebook with 5+ charts, each labeled (title, axis labels — no
  unlabeled charts, see the guide's pitfalls section)
- Each chart saved as a `.png` in `notebooks/reports/`
- A short written answer under each chart addressing the actual business
  question, not just a description of what's visible
- One paragraph at the end of the notebook: if you had to give leadership
  ONE headline finding from all five charts, what would it be and why

## Git workflow reminder
Commit as you build, not all at once:
```bash
git add notebooks/02_eda_visualization.ipynb notebooks/reports/
git commit -m "Add monthly revenue trend analysis"
# ...repeat per chart or logical group...
git push
```

Bring back the notebook (or a link to the pushed repo) when it's done —
partial is fine too if you get stuck on any single question. Once I'm
satisfied here, Phase 3 introduces basic statistics (correlation,
hypothesis testing) to go beyond "what happened" into "is this difference
actually meaningful, or just noise."
