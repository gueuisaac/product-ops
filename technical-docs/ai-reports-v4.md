# AI Reports - Technical Documentation

*All statements verified against actual implementation, not just type definitions.*

---

## Overview

AI Reports generates periodic insights from customer data using a two-stage AI pipeline (filtering + generation). Reports are delivered via Slack on configurable schedules.

**Entry point:** `crons/cmd/aireports/main.go:33`

---

## Data Sources

| Source | Status | Reference |
|--------|--------|-----------|
| Issues | Implemented | `reports/accessor.go:2269` |
| Call Recordings | Implemented | `reports/accessor.go:2280` |
| Manual Entries | Implemented | `reports/accessor.go:2285` |
| Activity Logs | Not implemented (TODO) | `reports/accessor.go:2290` |
| Internal Messages | Not implemented (TODO) | `reports/accessor.go:2293` |

---

## Processing Pipeline

**Stage 1 - Filtering:** GPT-5 Mini (`aireportinsights/accessor.go:799`)

| Limit | Value | Reference |
|-------|-------|-----------|
| Max issues | 50 | `aireportinsights/accessor.go:126` |
| Max call recordings | 10 | `aireportinsights/accessor.go:127` |
| Max manual entries | 10 | `aireportinsights/accessor.go:129` |
| Content truncate length | 1500 chars | `aireportinsights/accessor.go:124` |

**Stage 2 - Generation:** Claude Sonnet 4 via AWS Bedrock (`ai/prompts/aireportprompts/ai_report_insight.go:295`)

| Setting | Value | Reference |
|---------|-------|-----------|
| Max output tokens | 4096 | `ai_report_insight.go:293` |
| Default model | Claude Sonnet 4 | `ai_report_insight.go:295` |
| Cloud model | Bedrock Claude Sonnet 4 | `ai_report_insight.go:296` |

---

## Configuration

**Time Ranges** (`reporttypes/reporttypes.go:130-142`)

| Option | Value | Duration |
|--------|-------|----------|
| Last 1 day | `last_1_day` | 24h |
| Last 7 days | `last_7_days` | 168h |
| Last 1 month | `last_1_month` | 720h |
| Last 3 months | `last_3_months` | 2160h |

**Delivery Methods**

| Method | Status | Reference |
|--------|--------|-----------|
| Slack | Implemented | `reports/accessor.go:1761-1762` |
| Email | Not implemented (returns error) | `reports/accessor.go:1764` |

**Template Statuses** (`reporttypes/reporttypes.go:14-18`)

| Status | Value |
|--------|-------|
| Draft | `draft` |
| Published | `published` |
| Unpublished | `unpublished` |

---

## Database Tables

| Table | Model | Reference |
|-------|-------|-----------|
| `report_templates` | `ReportTemplate` | `models/reports.go:24` |
| `report_template_widgets` | `ReportTemplateWidget` | `models/reports.go:11` |
| `report_template_to_widget_layouts` | `ReportTemplateToWidgetLayout` | `models/reports.go:43` |
| `reports` | `Report` | `models/reports.go:85` |
| `report_widgets` | `ReportWidget` | `models/reports.go:107` |
| `ai_report_insights` | `AIReportInsight` | `models/reports.go:58` |

---

## Cron Execution Flow

1. Entry point calls `GenerateIntermediatesCron()` — `crons/cmd/aireports/main.go:33`
2. Acquires lock `aireportsintermediatelock` with 24h timeout — `reports/backfill.go:566`
3. Iterates all organizations in parallel (10 workers) — `reports/backfill.go:578`
4. For each published template, calls `GeneratePreviousDayIntermediatesForReportTemplate()` — `reports/backfill.go:587`
5. Calculates yesterday's period in template timezone — `reports/backfill.go:626-631`
6. Generates intermediates for AI widgets — `reports/backfill.go:639`

---

## Key Files

| File | Purpose |
|------|---------|
| `crons/cmd/aireports/main.go` | Cron entry point |
| `reports/backfill.go` | Cron orchestration logic |
| `reports/accessor.go` | Data fetching, report generation, delivery |
| `reports/aireportinsights/accessor.go` | AI pipeline and hyperparameters |
| `ai/prompts/aireportprompts/ai_report_insight.go` | Claude prompt definition |
| `reports/reporttypes/reporttypes.go` | Type definitions and constants |
| `models/reports.go` | Database model definitions |
