---
name: doc-to-dashboard
description: Takes a PDF, Excel, or CSV with tabular data and produces a self-contained HTML dashboard with headline insights, key metrics, flagged anomalies, and inline charts. Use when you have a spreadsheet or report gathering dust and want to know "what should I be paying attention to" without spending an afternoon on it. Works for invoices, defect logs, project schedules, training records, supplier spend, or any data with rows and columns.
---

# Doc-to-Dashboard

A skill for turning raw spreadsheets, CSVs, and PDF tables into a clear, self-contained HTML dashboard you can open in any browser, share by email, or print to PDF. Designed for managers who already have the data but don't have the bandwidth to make sense of it.

## When to use this skill

Invoke when you have:

- An Excel workbook from a department report
- A CSV export from your ERP, accounting system, or scheduling tool
- A PDF with tabular data (vendor list, defect log, training register)
- Data you've been "meaning to look at" but haven't

Typical triggers:

- "I need to understand what's in this before the management meeting"
- "What are the patterns in this data?"
- "What should I flag to my manager?"
- "Turn this into something I can share"

## What you (the user) provide

A short brief in the chat plus the file:

```
File: [attached or path]
Context: [one line — what is this data]
Audience: [optional — who will read the dashboard, default = me]
Focus: [optional — what you most want to know]
```

Examples:

- `Context: monthly accounts payable register / Audience: my manager / Focus: late payments`
- `Context: site defects logged in Q1 / Focus: recurring issues by contractor`
- `Context: training completion records / Audience: HR HOD / Focus: certifications expiring soon`

If `Context` is missing, ask once before generating. Without context, the dashboard will be generic and less useful.

## What you (Claude) produce

A single self-contained HTML file saved to `./dashboards/[filename]-dashboard.html`. Open it in any browser. No internet required.

The dashboard has six sections, top to bottom:

1. **Header** — title, date generated, source file name, one-line context
2. **Headline Insights** — 3 to 5 specific findings, each with a "why it matters" line
3. **Key Metrics** — totals, averages, distributions in clean tables
4. **Anomalies & Flags** — outliers, data quality issues, things that look off
5. **What You Should Notice** — 1-2 sentences per insight on what action to take
6. **Charts** — 1 to 2 inline SVG charts that visualize the most material pattern

## How Claude executes this skill

1. **Detect format** by file extension and magic bytes:
   - `.xlsx` / `.xls` → use `openpyxl` or `pandas.read_excel`
   - `.csv` → use `pandas.read_csv` (auto-detect delimiter and encoding)
   - `.pdf` → use `pdfplumber` to extract tables; fall back to `pypdf` text + heuristic parse if no tables found

2. **Infer structure**:
   - Detect header row (handle title rows above the actual headers)
   - Infer column types (text / number / currency / date / categorical)
   - Detect currency symbols (RM / USD / SGD / generic) — default to RM for Malaysian context
   - Detect date formats (DD/MM/YYYY and YYYY-MM-DD interchangeably; flag ambiguity)

3. **Run analysis**:
   - Descriptive stats per numeric column (count, sum, mean, median, std dev, min/max)
   - Outlier detection via IQR (1.5× rule) for numeric columns
   - Missing value scan
   - Duplicate detection on likely ID columns
   - Top-N concentration for categorical columns (e.g., top 5 suppliers by spend)
   - Date-range checks (records outside expected window flagged)
   - Cross-column relationships if obvious (e.g., due date vs paid date → days outstanding)

4. **Generate insights** using domain-aware reasoning:
   - Pull the 3-5 most material findings, prioritised by what `Audience` and `Focus` indicate
   - Each insight is specific, quantified, and traceable to source rows where possible
   - Each insight has a "why it matters" rationale

5. **Render HTML** using a print-safe template:
   - Minimum text contrast `#444` on white
   - Inline SVG for charts (no Chart.js, no external CDN)
   - `print-color-adjust: exact` for clean PDF export
   - Self-contained — opens offline, shares cleanly by email

6. **Save and open** — save to `./dashboards/[input-filename]-dashboard.html`. If on macOS, open it in default browser via `open`.

## Style rules

- Insights must be **specific and quantified**. "3 invoices over RM 50k from Supplier ABC are 60+ days overdue." Never "there are some issues in the data."
- Every flag includes **WHY it matters** — not just what's flagged.
- Currency formatted consistently (default RM, comma thousands separator, 2 decimals only when needed).
- Dates rendered as `DD MMM YYYY` for readability (e.g., "27 Apr 2026").
- Tables sorted by the most relevant column descending (cost, count, severity).
- HTML is print-safe — readable when printed to PDF, no light grey on white.
- No emoji in headings or insights (corporate context). Emoji acceptable for chart legend markers if clearer.
- HTML must be self-contained — no external dependencies, no CDN links, no fonts that need internet.

## Example invocation

User pastes:

```
File: monthly_ap_register_apr2026.xlsx
Context: monthly accounts payable register
Audience: my manager
Focus: late payments and supplier concentration
```

You:

1. Read the workbook, detect headers, infer types (Invoice ID / Supplier / Issue Date / Due Date / Amount RM / Status).
2. Identify late payments (Status = "Pending" + Due Date < today).
3. Compute supplier concentration (% of total spend by top 5 suppliers).
4. Flag anomalies (duplicate invoice IDs, dates outside the month's range, amounts above the IQR upper fence).
5. Generate 3-5 insights — e.g., "RM 1.2M outstanding past due from 4 suppliers" / "62% of monthly spend concentrated in top 3 suppliers" / "8 invoices missing Status field — needs cleanup before next cycle."
6. Render HTML with a horizontal bar chart of top suppliers by spend and a stacked bar of paid vs pending by week.
7. Save to `./dashboards/monthly_ap_register_apr2026-dashboard.html` and open it.

## Adapt for related departments

The base skill works on any tabular data. Department-aware defaults:

| Department | What the skill looks for by default |
|---|---|
| Finance / AP | Variance vs budget, aging, top vendor concentration, duplicate invoices |
| QAQC | Defect-type clusters, recurring contractors, severity distribution |
| Construction | Schedule slippage, milestone risks, sub-contractor performance |
| Procurement | Spend concentration, contract expiries, RFP candidates |
| HR | Completion rates, expiring certifications, training gaps |
| Property Mgmt | Open work orders, complaint clusters, response times |
| Customer Service | Ticket volume, escalation rates, resolution time |
| Planning | Schedule variance, resource utilisation, milestone alerts |

If `Context` matches one of these, lead the analysis with the relevant defaults. Otherwise, use generic descriptive analysis.

## What this skill is NOT for

- Confidential or PII-heavy data on public AI services. Use enterprise NotebookLM or an internal RAG setup for that — see your IT and governance teams.
- Real-time decision-making. Insights and flags are starting points for the human, not final calls.
- Long-form narrative reports. Use `report-skeleton` skill for that — different output shape.
- Predictive modelling. This is descriptive only — what's in the data, not what will happen.
- Charts that need interactivity. Output is static SVG. For interactive dashboards, that's a different stack (Tableau, Power BI, Looker Studio).

## Notes for skill authors

To adapt this skill for your team:

1. Replace the department adapter list with your firm's specific departments and their characteristic data shapes.
2. Edit the currency default if you operate outside Malaysia.
3. Add a brand colour to the HTML template's `--accent` variable for consistent firm-branded dashboards.
4. If your firm has standard chart preferences (e.g., always use bar charts, never pie), edit Step 6 of the execution sequence.
5. For confidential data, fork this skill and replace the Claude API call with an enterprise endpoint that has data-residency guarantees.

To use this skill in Claude Code, save this file as `SKILL.md` inside `.claude/skills/doc-to-dashboard/` in your project, or globally at `~/.claude/skills/doc-to-dashboard/`. Invoke it by mentioning the file you want analysed and the context.
