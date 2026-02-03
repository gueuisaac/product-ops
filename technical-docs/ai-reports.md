# AI Reports - Technical Documentation

*Generated from codebase analysis. All statements include code references.*

---

## Overview

AI Reports generates periodic insights from customer data using a two-stage AI pipeline. Reports are delivered via Slack or email on configurable schedules.

**Entry point:** `backend/go/src/pylon/crons/cmd/aireports/main.go:33`
```go
if err := reportsAccessor.GenerateIntermediatesCron(ctx); err != nil {
```

---

## Data Sources (Verified)

Data fetching occurs in `backend/go/src/pylon/reports/accessor.go:2249-2306` (`FetchRelevantDataForReport` function).

**Currently fetching data:**

| Source | DB Query Function | Code Reference |
|--------|-------------------|----------------|
| Issues | `GetIssuesByOrgIDAndAccountIDsHappenedBetween` | `accessor.go:2269` |
| Issues (all) | `GetIssuesByOrgIDHappenedBetween` | `accessor.go:2274` |
| Call Recordings | `GetCallRecordingsByAccountIDsAndTimeRange` | `accessor.go:2280` |
| Manual Entries | `GetManualEntriesForAccountsInTimeRange` | `accessor.go:2285` |

**NOT implemented (empty arrays with TODO comments):**

```go
// accessor.go:2290-2294
// TODO: Fetch activity logs for filtered accounts and time period
activityLogs := []accountactivitytypes.AccountActivity{}

// TODO: Fetch internal messages for filtered accounts and time period
internalMessages := []*models.MessageAssociation{}
```

---

## AI Pipeline

### Stage 1: Filtering (GPT-5 Mini)

**Model:** `FilterRelevantDataItemsForAIReportInsightGPT5Mini`  
**Code reference:** `backend/go/src/pylon/reports/aireportinsights/accessor.go:799`

**Filtering limits** (from `DefaultHyperparameters()` at `aireportinsights/accessor.go:112-138`):

| Parameter | Value | Code Line |
|-----------|-------|-----------|
| `MaxFilteredIssues` | 50 | `:126` |
| `MaxFilteredCallRecordings` | 10 | `:127` |
| `MaxFilteredManualEntries` | 10 | `:129` |
| `ContentTruncateLength` | 1500 | `:124` |

### Stage 2: Insight Generation (Claude Sonnet 4)

**Prompt:** `AIReportInsightReportClaude4Sonnet`  
**Code reference:** `backend/go/src/pylon/ai/prompts/aireportprompts/ai_report_insight.go:286-299`

```go
DefaultModel:     aimodels.ModelAnthropicClaude4SonnetV1,
CloudHostedModel: aimodels.ModelBedrockAnthropicClaude4SonnetV1,
MaxOutputTokens: 4096,
```

---

## Database Tables

From `backend/go/src/pylon/models/reports.go`:

| Table | Model | Primary Fields |
|-------|-------|----------------|
| `report_templates` | `ReportTemplate` | ID, OrganizationID, Title, Status, DeliveryMetadata, Schedule, DataTimeRange, Timezone |
| `report_template_widgets` | `ReportTemplateWidget` | ID, OrganizationID, Name, Config, WidgetType |
| `report_template_to_widget_layouts` | `ReportTemplateToWidgetLayout` | TemplateID, WidgetID, Row, ColumnStart, ColumnEnd |
| `reports` | `Report` | ID, TemplateID, Status, PeriodStart, PeriodEnd, DeliveryMetadata |
| `report_widgets` | `ReportWidget` | ID, ReportID, WidgetType, ContentHTML, MarkdownContentBlocks |
| `ai_report_insights` | `AIReportInsight` | ID, TemplateID, Scope, PromptHash, PeriodStart, PeriodEnd, ContentBlocks |

---

## Configuration Options

### Time Ranges

From `backend/go/src/pylon/reports/reporttypes/reporttypes.go:130-142`:

| Constant | Value | Duration |
|----------|-------|----------|
| `ReportDataTimeRangeLast1Day` | `"last_1_day"` | 24h |
| `ReportDataTimeRangeLast7Days` | `"last_7_days"` | 168h |
| `ReportDataTimeRangeLast1Month` | `"last_1_month"` | 720h |
| `ReportDataTimeRangeLast3Months` | `"last_3_months"` | 2160h |

### Delivery Methods

From `reporttypes/reporttypes.go:36-44`:

| Constant | Value |
|----------|-------|
| `ReportDeliveryMethodSlack` | `"slack"` |
| `ReportDeliveryMethodEmail` | `"email"` |

### Template Statuses

From `reporttypes/reporttypes.go:14-18`:

| Status | Value |
|--------|-------|
| `ReportTemplateStatusDraft` | `"draft"` |
| `ReportTemplateStatusPublished` | `"published"` |
| `ReportTemplateStatusUnpublished` | `"unpublished"` |

---

## Cron Execution Flow

1. **Entry:** `crons/cmd/aireports/main.go:33` calls `GenerateIntermediatesCron()`
2. **Lock acquisition:** `reports/backfill.go:566` - acquires `"aireportsintermediatelock"` with 24h timeout
3. **Org iteration:** `backfill.go:578` - iterates all organizations in parallel (10 workers)
4. **Template processing:** `backfill.go:584` - for each published template, calls `GeneratePreviousDayIntermediatesForReportTemplate()`
5. **Period calculation:** `backfill.go:626-631` - calculates yesterday's period in template timezone
6. **Widget generation:** `backfill.go:639` - calls `backfillAllWidgetsForDate()` for AI widgets

---

## Key Files

| File | Purpose |
|------|---------|
| `crons/cmd/aireports/main.go` | Cron entry point |
| `reports/backfill.go:563` | `GenerateIntermediatesCron()` - main cron logic |
| `reports/accessor.go:2249` | `FetchRelevantDataForReport()` - data fetching |
| `reports/aireportinsights/accessor.go:112` | `DefaultHyperparameters()` - filtering limits |
| `reports/aireportinsights/accessor.go:140` | `AIReportInsightsInput` struct |
| `ai/prompts/aireportprompts/ai_report_insight.go:286` | Claude Sonnet 4 prompt definition |
| `reports/reporttypes/reporttypes.go` | Type definitions and constants |
| `models/reports.go` | Database model definitions |

---

## Notes

- Activity Logs and Internal Messages fields exist in structs but data fetching is not implemented (TODO at `accessor.go:2290-2294`)
- The prompt schema (`ai_report_insight.go:46-126`) includes citation fields for all 5 data types, but only 3 are populated with data
