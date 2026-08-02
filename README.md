# RetailPulse — Sales Analytics & Forecasting

A fictional 5-store retail chain (Lagos, Abuja, Port Harcourt, Kano, Ibadan) needs
you to build out their analytics capability from scratch. This repo will grow
with you as we move through phases.

## Project structure
```
retailpulse/
├── data/
│   ├── raw/            <- original, untouched data lands here
│   └── processed/      <- your cleaned output goes here
├── notebooks/          <- exploration / scratch work
├── src/                <- reusable scripts/functions
└── README.md
```

## Dataset
`data/raw/sales_raw.csv` — ~29,600 transactions, Jan 2023–Dec 2024.

| Column | Description |
|---|---|
| transaction_id | unique ID per sale |
| date | transaction date |
| store | which of the 5 stores |
| category | product category |
| unit_price | price per unit |
| quantity | units sold (negative = return) |
| customer_age | age of customer |
| payment_method | how they paid |

This data is **intentionally messy** — that's the point of Task 1.

---

## PHASE 1 — TASK 1 (yours: git + pandas)

**Goal:** turn `sales_raw.csv` into a clean, analysis-ready dataset.

### Step 1 — Set up git
```bash
cd retailpulse
git init
git add .
git commit -m "Initial project structure and raw data"
```
(If you want, push it to a GitHub repo — this becomes portfolio piece #1.)

### Step 2 — Investigate (in a notebook or script)
Before fixing anything, document what's wrong. Run and note down:
- `df.info()` — check dtypes
- `df.isnull().sum()` — missing values per column
- `df.duplicated().sum()` — exact duplicate rows
- `df['unit_price'].apply(type).value_counts()` — mixed types lurking?
- `df['date'].str.contains('/').sum()` — inconsistent date formats?
- `df['payment_method'].unique()` — inconsistent categories?
- `df['quantity'].describe()` — anything odd (negative values)?
- `df['unit_price'].describe()` — outliers?

Write your findings into `notes/data_quality_report.md` — a short bullet list.
**This habit (audit before you clean) is one of the most important things
a data scientist does. Don't skip it even though it feels slow.**

### Step 3 — Clean it
Handle each issue you found. Guidance (not exact code — figure it out, that's
the point):

1. **`unit_price`**: some values are strings like `"₦3,509.17"`. Strip the
   currency symbol and commas, convert everything to float.
2. **`date`**: two formats mixed (`YYYY-MM-DD` and `DD/MM/YYYY`). Get it all
   into one consistent `datetime` dtype. Look at `pd.to_datetime` with the
   `format` and `errors` arguments, or try parsing both formats separately.
3. **Missing `unit_price`**: decide and justify a strategy — drop the rows,
   or impute (e.g. median price for that category)? There's no single
   "right" answer — pick one and explain why in your notes.
4. **Missing `customer_age`**: same decision process.
5. **Duplicate rows**: drop them — but check first whether they're true
   duplicates or coincidentally identical legitimate transactions.
6. **Negative `quantity`**: these are returns, not errors. Don't just delete
   them — think about whether to keep them as-is, flag them with a new
   column (e.g. `is_return`), or handle separately.
7. **Outlier prices** (a few rows ~100x normal): decide how to detect these
   (hint: look at category-level price distributions) and how to handle them.
8. **`payment_method`**: standardize inconsistent casing/spacing
   (`'CASH'`, `'Cash'`, `'Card '` should collapse to consistent values).

### Step 4 — Save & commit
- Save cleaned data to `data/processed/sales_clean.csv`
- Commit your work in **multiple small commits** as you go (not one giant
  commit at the end) — e.g. "Fix date formatting", "Handle missing prices",
  "Standardize payment methods". This is how git is actually used on a team.

### Deliverables to bring back to me:
1. `notes/data_quality_report.md`
2. `data/processed/sales_clean.csv`
3. Your cleaning code (script or notebook)
4. A one-paragraph summary: what was the messiest part, and what tradeoff
   did you make that you're least sure about?

That last question matters most — I want to see your reasoning, not just
correct output. I'll review it, and once I'm satisfied, we unlock Phase 2:
**visualization**, where you'll turn this clean data into a proper EDA
report using matplotlib/seaborn, and I'll hand you a learning resource for
that first.

No deadline pressure — go at your 2-4 hrs/week pace. Ping me when you've got
something, even partial, and I'll give feedback before you go further.
