# AI Reports - Technical Documentation

## Overview

AI Reports automatically generates periodic insights from customer conversations, call recordings, and activity data using a two-stage AI pipeline. Reports are delivered via Slack or email on configurable schedules.

---

## Data Sources

The following data sources are analyzed to generate insights:

- **Issues** - Customer support tickets and conversations
- **Call Recordings** - Transcribed customer calls
- **Activity Logs** - User actions and events
- **Manual Entries** - User-submitted data points
- **Internal Messages** - Team communications

---

## Data Flow

```
┌─────────────┐    ┌──────────────┐    ┌─────────────────┐    ┌──────────┐
│ Cron Job    │───▶│ Data Fetch   │───▶│ GPT-5 Mini      │───▶│ Claude   │
│ (Schedule)  │    │ (All Sources)│    │ (Filter/Rank)   │    │ Sonnet 4 │
└─────────────┘    └──────────────┘    └─────────────────┘    └────┬─────┘
                                                                   │
                                        ┌──────────────────────────┘
                                        ▼
                                   ┌──────────┐
                                   │ Delivery │
                                   │ (Slack/  │
                                   │  Email)  │
                                   └──────────┘
```

### Processing Steps

1. **Data Collection**: Cron job (`aireports/main.go`) triggers on schedule and gathers data from all sources within the configured time range.

2. **Filtering Stage**: GPT-5 Mini filters and ranks data for relevance.
   - Max Issues: 50
   - Max Call Recordings: 10
   - Max Activity Logs: 50
   - Max Manual Entries: 20
   - Max Internal Messages: 50

3. **Insight Generation**: Claude Sonnet 4 (via AWS Bedrock) analyzes filtered data and generates structured insights based on widget prompts.

4. **Delivery**: Report sent via configured channel (Slack or Email) with formatted insights.

---

## Key Files

| File | Purpose |
|------|---------|
| `backend/go/src/pylon/models/reports.go` | Database models (ReportTemplate, Report, ReportWidget, AIReportInsight) |
| `backend/go/src/pylon/reports/aireportinsights/accessor.go` | Core AI insights generation logic |
| `backend/go/src/pylon/ai/prompts/aireportprompts/ai_report_insight.go` | AI prompt templates |
| `backend/go/src/pylon/crons/cmd/aireports/main.go` | Cron job entry point |
| `backend/go/src/pylon/graphql/graph/schema.reports.graphqls` | GraphQL API schema |

---

## Database Tables

| Table | Description |
|-------|-------------|
| `report_templates` | Template definitions with schedule config |
| `report_template_widgets` | Widget configurations per template |
| `reports` | Generated report instances |
| `report_widgets` | Widget data per report |
| `ai_report_insights` | Cached AI-generated insights |

---

## Configuration

### Time Ranges
- `last_1_day` - Past 24 hours
- `last_7_days` - Past week
- `last_1_month` - Past month
- `last_3_months` - Past quarter

### Delivery Methods
- **Slack** - Posts to configured channel
- **Email** - Sends to configured recipients

### Schedule
Reports run on configurable cron expressions (e.g., daily, weekly).

---

## API / GraphQL

### Mutations
- `createReportTemplate` - Create a new report template
- `updateReportTemplate` - Update existing template

### Queries
- `reportTemplates` - List all templates
- `reportTemplate(id)` - Get single template
- `reports` - List generated reports
- `generateReportPreview` - Test report generation

---

## Dependencies

- **AWS Bedrock** - Claude Sonnet 4 model access
- **OpenAI API** - GPT-5 Mini for filtering
- **Slack API** - Report delivery
- **Email Service** - Report delivery

---

## How to Extend

### Add a New Data Source
1. Update `AIReportInsightsInput` struct in `accessor.go`
2. Add data fetching logic in the accessor
3. Update the AI prompt to include the new data type

### Add a New Widget Type
1. Add to `WidgetType` enum in `reporttypes/reporttypes.go`
2. Create new prompt template in `ai/prompts/aireportprompts/`
3. Add widget handling in the report generator

### Add a New Delivery Channel
1. Implement delivery interface in `reports/delivery/` package
2. Add channel type to delivery configuration
3. Update report template schema if needed