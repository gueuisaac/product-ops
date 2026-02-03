# AI Reports - Technical Documentation

*All statements verified against actual implementation.*

---

## Overview

AI Reports generates periodic insights from customer data using a two-stage AI pipeline and delivers them via Slack.

**Entry point:** `crons/cmd/aireports/main.go:33` → calls `GenerateIntermediatesCron()`

---

## Data Sources

| Source | Reference |
|--------|-----------|
| Issues | `reports/accessor.go:2269` |
| Call Recordings | `reports/accessor.go:2280` |
| Manual Entries | `reports/accessor.go:2285` |

---

## Processing Pipeline

**Stage 1 - Filtering:** GPT-5 Mini (`aireportinsights/accessor.go:799`)

| Setting | Value | Reference |
|---------|-------|-----------|
| Max issues | 50 | `aireportinsights/accessor.go:126` |
| Max call recordings | 10 | `aireportinsights/accessor.go:127` |
| Max manual entries | 10 | `aireportinsights/accessor.go:129` |
| Content truncate length | 1500 | `aireportinsights/accessor.go:124` |

**Stage 2 - Generation:** Claude Sonnet 4 (`ai/prompts/aireportprompts/ai_report_insight.go:295`)

| Setting | Value | Reference |
|---------|-------|-----------|
| Max output tokens | 4096 | `ai_report_insight.go:293` |
| Model | Bedrock Claude Sonnet 4 | `ai_report_insight.go:296` |

---

## Delivery

| Method | Reference |
|--------|-----------|
| Slack | `reports/accessor.go:1761-1762` |

---

## Time Ranges

| Option | Value | Reference |
|--------|-------|-----------|
| Last 1 day | `last_1_day` | `reporttypes/reporttypes.go:131` |
| Last 7 days | `last_7_days` | `reporttypes/reporttypes.go:132` |
| Last 1 month | `last_1_month` | `reporttypes/reporttypes.go:133` |
| Last 3 months | `last_3_months` | `reporttypes/reporttypes.go:134` |

---

## Database Tables

| Table | Model | Reference |
|-------|-------|-----------|
| report_templates | ReportTemplate | `models/reports.go:24` |
| report_template_widgets | ReportTemplateWidget | `models/reports.go:11` |
| reports | Report | `models/reports.go:85` |
| report_widgets | ReportWidget | `models/reports.go:107` |
| ai_report_insights | AIReportInsight | `models/reports.go:58` |

---

## Execution Flow

1. Cron entry → `crons/cmd/aireports/main.go:33`
2. Acquire lock (24h timeout) → `reports/backfill.go:566`
3. Iterate orgs (10 parallel workers) → `reports/backfill.go:578`
4. Get published templates → `reports/backfill.go:579`
5. Calculate yesterday's period → `reports/backfill.go:629-631`
6. Generate intermediates → `reports/backfill.go:639`

---

## Key Files

| File | Purpose |
|------|---------|
| `crons/cmd/aireports/main.go` | Cron entry point |
| `reports/backfill.go` | Cron orchestration |
| `reports/accessor.go` | Data fetching, delivery |
| `reports/aireportinsights/accessor.go` | AI pipeline |
| `ai/prompts/aireportprompts/ai_report_insight.go` | Prompt definition |
| `models/reports.go` | Database models |
