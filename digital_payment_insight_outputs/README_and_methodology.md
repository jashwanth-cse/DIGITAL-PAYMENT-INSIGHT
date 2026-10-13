# Digital Payment Insight — Outputs and Methodology

## Source
Kaggle competition: https://www.kaggle.com/competitions/behavioral-fraud-detection
Training file used: `/root/.cache/kagglehub/competitions/behavioral-fraud-detection/train.csv`
Rows: 182,125; columns: 10.

## Main outputs
- `transactions.csv`: cleaned source transactions plus engineered features and synthetic merchant link.
- `customers.csv`: customer activity segment derived from transaction count; region and tenure are synthetic.
- `devices.csv`: transaction-device events; device type is synthetic; new-device flag is a first-seen user-device proxy within this training file.
- `merchants.csv`: synthetic merchant IDs and synthetic regions linked to source merchant-category codes.
- `alerts.csv`: simulated rule-based review queue generated without using the source fraud label.
- `cleaned_master_transactions.csv`: joined analysis table.
- `data_quality_report.csv`: original-source vs controlled-working-copy vs cleaned results.
- `Digital_Payment_Insight_Analysis.xlsx`: workbook with linked data, summaries, charts, formulas, and a PivotTable guide.
- `Digital_Payment_Insight_Business_Pitch.pptx`: short business pitch.
- `business_pitch_speaker_notes.md`: speaking notes and limitations.
- `charts/`: saved figures used in the workbook/pitch.

## Cleaning and data-quality simulation
The original source was audited separately. This notebook introduces missing merchant categories, missing device IDs, inconsistent channel label variants, and duplicate transaction records into a reproducible working copy because the assessment names these conditions. These are simulated conditions, not claims about the original source. Duplicate transaction IDs are dropped; channel values are normalized; missing merchant categories are labeled `unknown`; missing device IDs are retained and flagged. Amount IQR outliers are flagged, not removed.

## Interpretation limits
- `timestamp` is retained as a numeric relative value. Elapsed-hour bins assume seconds for exploratory plotting; the source time unit/reference is not verified. Do not describe these bins as actual hour-of-day patterns.
- `hours_since_prev_txn` is preserved exactly. Its name may not match its unit; analyses use it only as a supplied numeric gap for a low-tail flag.
- Source channel, merchant-category and country values are encoded numbers. Neutral code labels are used; no unverified mapping is invented.
- Synthetic customer regions/tenure, device types, merchant IDs/regions and alert queue statuses are not source facts.
- Alerts use amount, first-seen-device proxy, low-tail supplied gap and missing-device flags. They do not use `label`. Alert reason categories/statuses are simulated, not real manual review outcomes.
- An observed fraud-label rate is descriptive association, not causal evidence.

## Snapshot
- Transactions: 182,125
- Customers: 5,000
- Observed device IDs: 8,743
- Synthetic merchants: 210
- Synthetic alerts: 16,706 (9.17% of transactions)
- Source fraud-label rate: 1.64%
- Median source transaction amount: 20.07

## Excel PivotTables
The workbook includes a `PivotTable Guide` sheet with exact field setups. The grouped summary tabs are precomputed summaries, not native PivotTables. To meet the native PivotTable requirement, open the workbook in desktop Excel, select a cell in `Analysis Data`, choose Insert → PivotTable, then follow the guide. Add a PivotChart for each required view.
