# AI Reports - Technical Documentation

*All statements verified against actual implementation.*

---

## Overview

AI Reports generates periodic insights from customer data through a multi-stage process: daily intermediate insights are generated and stored, then combined into a final report when delivered via Slack.

**Entry point:** `crons/cmd/aireports/main.go:33`

---

## How It Works

### Stage 1: Daily Intermediate Generation

A cron job runs daily to generate intermediate insights for each day's data.

| Step | Description | Reference |
|------|-------------|-----------|
| 1 | Acquire lock (24h timeout) | `reports/backfill.go:566` |
| 2 | Iterate all orgs (10 parallel workers) | `reports/backfill.go:578` |
| 3 | Get published templates per org | `reports/backfill.go:579` |
| 4 | Calculate yesterday's period in template timezone | `reports/backfill.go:629-631` |
| 5 | Fetch data for period | `reports/accessor.go:2249` |
| 6 | Filter with GPT-5 Mini | `aireportinsights/accessor.go:799` |
| 7 | Generate insight with Claude Sonnet 4 | `ai/prompts/aireportprompts/ai_report_insight.go:295` |
| 8 | Store as intermediate insight | `models/reports.go:58` |

### Stage 2: Final Report Generation

When a report is sent, intermediate insights are combined into a final report.

| Step | Description | Reference |
|------|-------------|-----------|
| 1 | Fetch intermediates for time range | `reports/accessor.go:1525` |
| 2 | Sort intermediates by period start | `reports/accessor.go:1618` |
| 3 | Format intermediates as XML blocks | `reports/accessor.go:1628-1688` |
| 4 | Call Claude Sonnet 4 to combine | `reports/accessor.go:1710` |
| 5 | Parse and format final content blocks | `reports/accessor.go:1735-1743` |

**Combination prompt:** `GenerateReportFromIntermediatesClaude4Sonnet` (`reports/accessor.go:1710`)

### Stage 3: Delivery

| Step | Description | Reference |
|------|-------------|-----------|
| 1 | Check delivery mode is Slack | `reports/accessor.go:1761` |
| 2 | Get Slack channel IDs | `reports/accessor.go:1771` |
| 3 | Convert widgets to Slack blocks | `reports/accessor.go:1783` |
| 4 | Send to each channel | `reports/accessor.go:1800` |

---

## Data Sources

| Source | Reference |
|--------|-----------|
| Issues | `reports/accessor.go:2269` |
| Call Recordings | `reports/accessor.go:2280` |
| Manual Entries | `reports/accessor.go:2285` |

---

## Filters

Filters are applied at two levels:

| Level | What's Filtered | Reference |
|-------|-----------------|-----------|
| Account | Accounts matching filter criteria | `reports/accessor.go:2318` |
| Issue | Issues matching filter criteria | `reports/accessor.go:2296` |

**Filter structure:** `filtertypes.Filters` supports AND (`AllOf`) and OR (`AnyOf`) conditions (`filter/filtertypes/filtertypes.go:32-37`)

**Custom fields supported:** Yes (`filter/filtertypes/filtertypes.go:59-71`)

**When filters change:** All intermediate insights are deleted and regenerated (`reports/backfill.go:101-103`)

---

## Processing Limits

| Setting | Value | Reference |
|---------|-------|-----------|
| Max issues | 50 | `aireportinsights/accessor.go:126` |
| Max call recordings | 10 | `aireportinsights/accessor.go:127` |
| Max manual entries | 10 | `aireportinsights/accessor.go:129` |
| Content truncate length | 1500 chars | `aireportinsights/accessor.go:124` |
| Max output tokens | 4096 | `ai_report_insight.go:293` |

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

| Table | Purpose | Reference |
|-------|---------|-----------|
| report_templates | Template config, filters, schedule | `models/reports.go:24` |
| report_template_widgets | Widget config per template | `models/reports.go:11` |
| ai_report_insights | Stores intermediate and final insights | `models/reports.go:58` |
| reports | Generated report instances | `models/reports.go:85` |
| report_widgets | Widget content per sent report | `models/reports.go:107` |

**Insight scopes:** `intermediate` (daily), `template_preview`, `report_run` (`reporttypes/reporttypes.go:121-124`)

---

## Key Files

| File | Purpose |
|------|---------|
| `crons/cmd/aireports/main.go` | Cron entry point |
| `reports/backfill.go` | Intermediate generation orchestration |
| `reports/accessor.go` | Data fetching, filtering, final report generation, delivery |
| `reports/aireportinsights/accessor.go` | AI pipeline for intermediate insights |
| `ai/prompts/aireportprompts/ai_report_insight.go` | Prompt for intermediate generation |
| `filter/filtertypes/filtertypes.go` | Filter structure and validation |
| `models/reports.go` | Database models |
