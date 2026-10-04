# Tableau Public dashboard: build guide

Four sheets, one dashboard, about 60 to 90 minutes. Everything reads from `output/llm/csv/`.

## 0. Setup
1. Create a free Tableau Public account and install Tableau Public Desktop.
2. Connect > Text file > `kpis.csv`. Add `guidance_tracker.csv`, `guidance_scorecard.csv` and `analyst_topics.csv` as separate data sources.
3. In every source, filter `status = grounded` where the column exists. Only verified facts reach the dashboard.

## Sheet 1: KPI trends (kpis.csv)
- Columns: `quarter` (sort by a calculated field `INT(MID([quarter],5,2))*4 + INT(MID([quarter],2,1))`).
- Rows: `value_pct`. Colour: `bank`. Filter: `metric` (show as a single-value dropdown; default `nim`).
- Tooltip: add `evidence`, so hovering a point shows the sentence management actually said.

## Sheet 2: Guidance scorecard (guidance_scorecard.csv)
- Horizontal bars: `bank` on rows, `delivery_rate` on columns, sorted descending.
- Label each bar with `delivered` / `resolved`, e.g. "6 of 8".
- Title: "How often management delivered what it guided".

## Sheet 3: Guidance detail (guidance_tracker.csv)
- Text table: bank, quarter, metric, guided band (`low_pct` to `high_pct` or `direction`), `observed_pct`, `status`.
- Colour `status`: delivered = green, missed = red, pending = grey.

## Sheet 4: What analysts asked (analyst_topics.csv)
- Heatmap: `topic` on rows, `quarter` on columns, `COUNT(text)` as colour. Filter: `bank`.
- Reading: rising squares show where the market's worry is moving (for example asset quality after a slippage quarter).

## Dashboard
- Layout: Sheet 2 top left, Sheet 1 top right, Sheet 4 bottom left, Sheet 3 bottom right.
- Add a global `bank` filter applied to all sheets.
- Add a text box: "Every figure is verified word for word against the bank's transcript. Source: company earnings call transcripts."
- File > Save to Tableau Public. Copy the public link into your CV and the GitHub README.
