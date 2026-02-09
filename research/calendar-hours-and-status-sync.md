# Calendar Hours and Status Sync: PRD Research Baseline

*Generated: 2026-02-09*
*Last Updated: 2026-02-09*

## Summary

Calendar Hours and Status Sync enables support agents to control their busy/active status at a personal level through two mechanisms: (1) manually setting their own timezone and support hours on their personal settings page, and (2) automatically syncing busy status from their connected Google or Outlook calendar when they have a meeting. This eliminates the need for agents to manually toggle their status throughout the day, ensures routing and assignment decisions reflect real-time availability, and supports distributed teams across timezones.

**Key constraint:** Google Calendar's API does not expose working hours settings (open issue since 2022). This is why personal working hours must be set manually within Pylon, while calendar sync handles meeting-level busy detection via the freebusy API.

---

## Competitive Analysis

### Salesforce Service Cloud — "Omni-Channel Presence"

- **Feature name:** Omni-Channel Presence & Shifts
- **How it works:** Agents set their availability through the Omni-Channel widget in the Service Console. Admins define Presence Statuses (Online, Busy, custom statuses) and Presence Configurations that control capacity per channel. Agents manually select their status; supervisors monitor via Omni Supervisor dashboard showing real-time presence, capacity, and time-in-status. Shifts can be defined with start/end times to align agent availability with service hours.
- **Key capabilities:**
  - Manual status toggle via Omni-Channel widget (Online, Busy, Offline, custom)
  - Presence Configurations set capacity limits per agent per channel
  - Omni Supervisor dashboard shows real-time agent presence, assigned work, capacity
  - Shift scheduling with start/end times for agent groups
  - Idle timeout: configurable auto-away after inactivity
  - Status-Based Capacity routing considers agent presence for work assignment
  - Offline agent tracking added in Spring '26
- **Calendar integration:** No native calendar sync for agent status. Third-party WFM tools (Dialed, Playvox) integrate via AppExchange for shift scheduling.
- **Timezone/hours:** Shifts are org/group-level, not per-agent personal hours. Individual timezone display is supported but does not drive availability.
- **Limitations:**
  - No automatic status sync from Google/Outlook calendar
  - Shifts are group-based, not personal per-agent hours
  - Requires third-party WFM tools for advanced scheduling
- **Pricing tier:** Omni-Channel included in Service Cloud Enterprise ($165/user/month) and above. Shifts available at Enterprise+.
- **Sources:**
  - [Route Work with Omni-Channel](https://help.salesforce.com/s/articleView?id=service.omnichannel_intro.htm&language=en_US&type=5)
  - [Omni-Channel for Administrators (Spring '26 PDF)](https://resources.docs.salesforce.com/latest/latest/en-us/sfdc/pdf/service_presence_administrators.pdf)
  - [Salesforce Omni-Channel Setup Guide](https://astreait.com/Omni-Channel-in-Salesforce-Service-Cloud/)
  - [Shifts in Salesforce Service Cloud](https://astreait.com/Shifts-in-Salesforce-Service-Cloud/)
  - [Best practices for Status-Based Capacity](https://unofficialsf.com/best-practices-for-status-based-capacity/)

### Zendesk — "Unified Agent Statuses"

- **Feature name:** Unified Agent Statuses
- **How it works:** Agents set their status (Online, Away, Offline, plus custom statuses) from the agent interface. Admins define custom statuses and configure idle timeout rules. Agents can view their schedule, request time off, and trade shifts. Account-level timezone is the default; agents can switch their schedule view to a different timezone for personal convenience (display only, does not affect routing).
- **Key capabilities:**
  - Manual status toggle (Online, Away, Offline, Transfer Only, custom)
  - Unified statuses across Talk, Chat, and Messaging channels
  - Idle timeout: configurable auto-away with default or custom idle status
  - Schedule management: agents view shifts, request time off, trade shifts
  - AI agent can check operating hours and agent availability before handoff
  - Agent availability time tracking for reporting
- **Calendar integration:** No native Google/Outlook calendar sync. Schedule management is internal to Zendesk (WFM add-on or third-party like Assembled).
- **Timezone/hours:** Account-level timezone. Agents can change their schedule view timezone (display only). Business hours/schedules are org-level, not per-agent.
- **Limitations:**
  - No automatic status from external calendar
  - Personal working hours not configurable per agent (org-level schedules only)
  - WFM features require additional add-on
- **Pricing tier:** Unified Agent Statuses available on Suite Professional ($115/agent/month) and above. WFM is a separate add-on.
- **Sources:**
  - [Managing unified agent statuses](https://support.zendesk.com/hc/en-us/articles/5133588225690-Managing-the-unified-agent-statuses-available-to-your-agents)
  - [Configuring idle timeout settings](https://support.zendesk.com/hc/en-us/articles/5286614817562-Configuring-idle-timeout-and-disconnection-settings-for-unified-agent-statuses)
  - [Viewing and managing your schedule as an agent](https://support.zendesk.com/hc/en-us/articles/6443374353434-Viewing-and-managing-your-schedule-as-an-agent)
  - [Which time zone does Zendesk use?](https://support.zendesk.com/hc/en-us/articles/4408821092762-Which-time-zone-does-Zendesk-use)
  - [Checking operating hours and agent availability with AI agents](https://support.zendesk.com/hc/en-us/articles/8357749686554-Checking-operating-hours-and-agent-availability-during-conversations-with-advanced-AI-agents)

### Intercom — "Teammate Availability"

- **Feature name:** Teammate Availability / Away Mode
- **How it works:** Teammates toggle between Available and Away from the inbox. Admins can configure automatic away mode based on inactivity thresholds. Custom away reasons can be created and required. Office hours are set at the workspace or team inbox level, not per-individual.
- **Key capabilities:**
  - Manual Available/Away toggle from inbox
  - Custom away reasons (customizable, can be required)
  - Automatic away mode: configurable inactivity threshold triggers Away status
  - Away & reassign: optionally reassign conversations when going Away
  - Office hours per team inbox (not per teammate)
  - Phone availability management (separate from chat/messaging status)
  - Away reasons settable via API for automation
- **Calendar integration:** No native calendar sync. Calendly integration exists for scheduling meetings from Messenger, but does not affect agent availability status.
- **Timezone/hours:** Office hours are team-level only. Per-teammate office hours is an open community request that has not been fulfilled.
- **Limitations:**
  - Cannot set custom office hours per individual teammate (team inbox only)
  - No automatic status from calendar events
  - No personal working hours configuration
- **Pricing tier:** Available on all plans: Essential ($29/seat/mo), Advanced ($85/seat/mo), Expert ($132/seat/mo). Custom away reasons on Advanced+.
- **Sources:**
  - [Manage teammate inbox status](https://www.intercom.com/help/en/articles/6522874-manage-teammate-inbox-status)
  - [Automatic away mode](https://www.intercom.com/help/en/articles/6899988-automatic-away-mode)
  - [Set your default office hours](https://www.intercom.com/help/en/articles/732390-let-customers-know-you-re-out-of-office)
  - [Customize your away reasons](https://www.intercom.com/changes/en/87197-customize-your-away-reasons-for-better-team-management)
  - [Can I set office hours for individual teammates? (community request)](https://community.intercom.com/messenger-8/can-i-set-office-hours-for-individual-teammates-1492)

### HubSpot — "Working Hours" (BEST-IN-CLASS for per-user hours)

- **Feature name:** Working Hours & Availability
- **How it works:** Each user sets their own working hours and timezone in their personal preferences (Users & Teams settings). The system automatically toggles their status to Available at the start of their working hours and Away at the end. Outside working hours, users are ineligible for auto-assignment. Manual overrides are available at any time.
- **Key capabilities:**
  - Per-user working hours with day-by-day configuration
  - Per-user timezone with optional auto-detection from device
  - Automatic Available/Away toggle based on working hours
  - Manual override available at any time from Inbox or Help Desk
  - Affects auto-assignment eligibility (not assigned outside hours)
  - Out of office hours management (separate from working hours)
  - Availability Management permissions for managers to adjust others' status
  - Working hours displayed on user profile
- **Calendar integration:** No native Google/Outlook calendar sync for busy status during meetings.
- **Timezone/hours:** Fully per-user. Each user sets their own timezone and daily working hours.
- **Limitations:**
  - No calendar-based busy detection during meetings
  - No shift management for teams (individual-only)
  - No idle detection / auto-away based on inactivity
- **Pricing tier:** Available on all products and plans (not premium-gated).
- **Sources:**
  - [Manage user working hours and availability](https://knowledge.hubspot.com/user-management/manage-user-working-hours-for-inbox-and-help-desk)
  - [Manage user availability for help desk](https://knowledge.hubspot.com/help-desk/manage-user-availability-for-help-desk)
  - [Manage user out of office hours](https://knowledge.hubspot.com/help-desk/manage-user-out-of-office-hours-for-inbox-and-help-desk)
  - [Manage user availability for conversations inbox](https://knowledge.hubspot.com/inbox/manage-your-inbox-users)

### Front — "Shifts" (Enterprise only)

- **Feature name:** Shifts
- **How it works:** Workspace-level shift schedules that automatically manage teammate availability. When a shift starts, teammates are set to Available; when it ends, they are set to Out of Office. Assignment rules automatically skip teammates not on a current shift. If a customer replies to a conversation assigned to an out-of-office teammate, the conversation is unassigned to the shared inbox.
- **Key capabilities:**
  - Automatic Available/Out of Office based on shift schedule
  - Workspace-level shifts with multiple teammates per shift
  - Multi-timezone support (create shifts for different zones)
  - Manual override: teammates can change status at any time
  - Assignment rules respect shift schedules
  - Time off integration with Front's native time off feature
  - Shifts API for custom integrations
- **Calendar integration:** No native external calendar integration. Shifts only use Front's native time off feature. Teams can use Front's API to build custom integrations with third-party scheduling.
- **Timezone/hours:** Workspace-based shifts, not per-user personal hours. Multiple shifts can reflect different timezones.
- **Limitations:**
  - Enterprise plan only ($105/user/month billed annually)
  - No external calendar sync (Google/Outlook)
  - Shift-based (group), not individual working hours
  - No meeting-level busy detection
- **Pricing tier:** Enterprise only ($105/user/month billed annually).
- **Sources:**
  - [Use shifts to manage work schedules](https://help.front.com/en/articles/2246)
  - [Workforce Management](https://help.front.com/en/articles/3327616)
  - [Shifts API Reference](https://dev.frontapp.com/reference/shifts)

### Freshdesk — "Agent Shifts"

- **Feature name:** Agent Shifts
- **How it works:** Shifts are configured at the group level. Admins name the shift, select a timezone, set specific days and times, and add agents. Agent availability is automatically changed based on shift hours. Automation rules can assign inquiries only to agents during their shift and reassign tickets when agents go offline.
- **Key capabilities:**
  - Group-based shift scheduling with timezone per shift
  - Automatic availability toggle based on shift hours
  - Automation rules for shift-aware ticket routing
  - Reassignment when agents become unavailable
  - Business Hours (separate from shifts) for SLA calculations
- **Calendar integration:** Third-party calendar apps available in Freshworks Marketplace, but no native calendar sync for agent status.
- **Timezone/hours:** Group-based shifts with timezone per shift. Not per-individual agent.
- **Limitations:**
  - Enterprise plan only
  - Group-based, not personal per-agent hours
  - No external calendar integration for busy detection
- **Pricing tier:** Enterprise plan only (Freshdesk Enterprise, Freshdesk Omni Enterprise).
- **Sources:**
  - [Setting up agent shifts in Freshdesk](https://support.freshdesk.com/support/solutions/articles/50000003157-setting-up-agent-shifts-in-freshdesk)
  - [What are business hours and calendar hours?](https://support.freshdesk.com/support/solutions/articles/37627-what-are-business-hours-and-calendar-hours-)

### Help Scout — "Office Hours"

- **Feature name:** Office Hours
- **How it works:** Company-level office hours set from Manage > Company > Office Hours. Toggle status on, enter hours per day. Can apply to all inboxes or specific ones. Per-user timezone exists for display purposes (conversation timestamps). Office hours are used for SLA reporting, not for agent availability toggling.
- **Key capabilities:**
  - Company-level office hours with per-day configuration
  - Per-inbox application (all or specific)
  - Per-user timezone for display (profile setting)
  - Office hours filtering in Email Report and User Report
- **Calendar integration:** None.
- **Timezone/hours:** Company-level office hours. Per-user timezone for display only.
- **Limitations:**
  - No per-user working hours
  - No automatic status management based on hours
  - No calendar integration
  - Office hours only used for reporting, not routing
- **Pricing tier:** Available on Standard ($25/user/month) and above.
- **Sources:**
  - [Set Company Office Hours](https://docs.helpscout.com/article/503-set-company-office-hours)
  - [Manage Company Settings](https://docs.helpscout.com/article/1408-manage-company-settings)
  - [Manage Your User Profile](https://docs.helpscout.com/article/499-manage-your-user-profile)

### Common Patterns

| Capability | Salesforce | Zendesk | Intercom | HubSpot | Front | Freshdesk | Help Scout |
|---|---|---|---|---|---|---|---|
| Manual status toggle | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ❌ |
| Per-user working hours | ❌ | ❌ | ❌ | ✅ | ❌ | ❌ | ❌ |
| Auto Available/Away from hours | ❌ | ❌ | ❌ | ✅ | ✅ (shifts) | ✅ (shifts) | ❌ |
| Per-user timezone | Display only | Display only | ❌ | ✅ (drives routing) | ❌ | ❌ | Display only |
| Google Calendar busy sync | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| Outlook Calendar busy sync | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| Idle detection / auto-away | ✅ | ✅ | ✅ | ❌ | ❌ | ❌ | ❌ |
| Shift management (group) | ✅ | Add-on | ❌ | ❌ | ✅ (Enterprise) | ✅ (Enterprise) | ❌ |
| Status affects assignment | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ❌ |
| Issue reassignment on status change | ✅ | ❌ | ✅ (optional) | ❌ | ✅ | ✅ | ❌ |
| Custom status reasons | ✅ | ✅ | ✅ | ❌ | ❌ | ❌ | ❌ |

### Key Insight

**No platform natively reads Google/Outlook calendar busy/free status to set agent availability.** This is a genuine white space across the entire support platform market. HubSpot leads on per-user working hours with automatic status toggling (available on all plans), but even HubSpot does not sync with external calendars for meeting-level busy detection. Building both per-user working hours AND calendar busy sync would give Pylon a unique combination that no competitor offers.

---

## Google Calendar API: Working Hours Limitation

### Confirmed: Working Hours Not Exposed via API

Google Calendar allows users to set working hours in their calendar settings, but this data is **not accessible through the Calendar API**. This is confirmed by multiple open issues on Google's issue tracker:

- **[Issue #181655431](https://issuetracker.google.com/issues/181655431)** — "Calendar API for Working Hours" — Feature request to "Create an API to retrieve working hours, or include this information in the free/busy api results." Not implemented.
- **[Issue #231620767](https://issuetracker.google.com/issues/231620767)** — "Expose Working Hours within API" — References three previously closed popular requests. Google stated it "wasn't a priority," preventing further community voting.

### Working Location vs Working Hours

Google did add **Working Location** to the Calendar API (where someone is physically working from), but **Working Hours** (when someone is available) remain unavailable. Working hours and location features are only available for Google Workspace accounts.

### Freebusy API as Workaround

The **freebusy.query** endpoint (`POST https://www.googleapis.com/calendar/v3/freeBusy`) can determine if someone is currently in a meeting:
- Request: `timeMin`, `timeMax`, calendar IDs
- Response: Array of `busy` blocks with `start` and `end` timestamps
- If current time falls within a busy block, the person is in a meeting
- Does NOT return meeting titles, details, or working hours preferences
- Requires `calendar.readonly` or `calendar.freebusy` OAuth scope

**Sources:**
- [Google Issue Tracker #181655431](https://issuetracker.google.com/issues/181655431)
- [Google Issue Tracker #231620767](https://issuetracker.google.com/issues/231620767)
- [Freebusy: query API Reference](https://developers.google.com/workspace/calendar/api/v3/reference/freebusy/query)
- [Set your working hours & location](https://support.google.com/calendar/answer/7638168?hl=en)
- [Use working locations with the Calendar API](https://developers.googleblog.com/en/use-working-locations-with-the-calendar-api-for-apps-and-workflows/)

### Microsoft Graph API: Working Hours ARE Exposed

Unlike Google, Microsoft's Graph API **does** expose working hours via the [mailboxSettings resource](https://learn.microsoft.com/en-us/graph/api/resources/mailboxsettings):
- `GET /me/mailboxSettings` returns `workingHours` object with `daysOfWeek`, `startTime`, `endTime`, `timeZone`
- This means Outlook Calendar integration could read both working hours AND meeting busy status

---

## Current Pylon Implementation

### User Status System

| Component | Details | Reference |
|---|---|---|
| Status enum | `Active`, `Away`, `OutOfOffice` (+ `Undefined` default) | `backend/go/src/pylon/person/users/usertypes/usertypes.go:160-170` |
| User model fields | `Status`, `StatusUntilTime` (nullable timestamp for timed status) | `backend/go/src/pylon/models/user.go:24-25` |
| Database index | `idx_organization_id_status_until_time` for efficient timed status queries | `backend/go/src/pylon/models/user.go:15` |
| GraphQL mutation | `setUserStatus(input: SetUserStatusInput!)` with status, statusUntilTime, optional issue reassignment | `backend/go/src/pylon/graphql/graph/schema.user.graphqls:111, 163-176` |
| Resolver | Parses RFC3339 timestamp, authorization check, optional async issue reassignment | `backend/go/src/pylon/graphql/graph/schema.user.resolvers.go:602-660` |
| Status detector | Background poller (every 1 minute) that reverts expired timed statuses back to Active | `backend/go/src/pylon/person/users/userstatusdetector/user_status_detector.go` |

### SetUserStatus Mutation Input

```graphql
input SetUserStatusInput {
  organizationID: String!
  userID: String!
  status: String!
  statusUntilTime: String           # RFC3339 timestamp for timed status

  shouldReassignOpenIssues: Boolean  # Reassign issues when going Away/OOO
  fromUserID: String
  toUserID: String
  updateTeam: Boolean
  reassignToExistingTeam: Boolean
  toTeamID: String
}
```

### Calendar Integrations

| Integration | Scopes | Key Capabilities | Reference |
|---|---|---|---|
| Google Calendar | `CalendarEventsReadonlyScope`, `CalendarReadonlyScope`, openid, profile, email | GetCalendarList, GetPrimaryCalendar, GetCalendarEvents, GetCalendarEvent, SearchCalendarEventsByMeetingCode, CreateSubscription (webhooks) | `backend/go/src/pylon/externalsystem/calendar/googlecalendar/client.go:20-66` |
| Outlook Calendar | `Calendars.Read`, `Calendars.Read.Shared`, openid, offline_access, profile, email | GetCalendarList, GetPrimaryCalendar, GetCalendarEvents, GetCalendarEvent, CreateSubscription, DeleteSubscription | `backend/go/src/pylon/externalsystem/calendar/outlookcalendar/client.go:25-43` |

Both integrations:
- Filter private/confidential events
- Store OAuth tokens on ExternalUser model (encrypted)
- Support webhook subscriptions for real-time event changes

### OAuth Token Storage

```go
// backend/go/src/pylon/models/external_user.go
func (e *ExternalUser) GetGoogleCalendarToken() *string
func (e *ExternalUser) GetGoogleRefreshToken() *string
func (e *ExternalUser) GetOutlookCalendarToken() *string
```

Tokens stored as encrypted strings in `ExternalUserMetadata` on the `ExternalUser` model (`backend/go/src/pylon/models/external_user.go:10-53`).

### Assignment Routing & Busy Status

The assignment system already considers user status when routing issues:

```go
// backend/go/src/pylon/triggers/actionexecutor/executor.go:959-966
if vars.OnlyAssignIfActive && !assigneeUser.IsActive() {
    switch assigneeUser.Status {
    case usertypes.Away:
        reason = eventlogmetadata.IssueAssignedSkippedReasonAssigneeBusy
    case usertypes.OutOfOffice:
        reason = eventlogmetadata.IssueAssignedSkippedReasonAssigneeOOO
    }
}
```

Skip reasons tracked in event log (`backend/go/src/pylon/core/eventlog/eventlogmetadata/issue.go:390-410`):
- `assignee_busy` — Agent is Away
- `assignee_ooo` — Agent is Out of Office
- `already_assigned` — Issue already has an assignee
- `assignee_deactivated` — Agent account deactivated
- `agent_disabled` — Agent disabled
- `agent_qamode` — Agent in QA mode

### Existing Support Hours UI

| File | Purpose |
|---|---|
| `frontend/src/pages/app/settings/support-hours/SupportHours.tsx` | Main support hours settings page |
| `frontend/src/pages/app/settings/support-hours/ModifySupportHours.tsx` | Create/edit support hours configuration |
| `frontend/src/pages/app/settings/support-hours/SupportHoursCalendar.tsx` | Calendar view for support hours |

These are **organization-level** support hours (business hours), not per-user personal hours.

### Timezone Infrastructure

| Component | Details | Reference |
|---|---|---|
| TimezoneSelector | React component with 400+ IANA timezone options | `frontend/src/common/components/timezone-selector/TimezoneSelector.tsx` |
| UserSettings | Includes preferred language but does NOT include personal timezone | `backend/go/src/pylon/person/users/usertypes/usertypes.go:81-93` |

### What Does NOT Exist

- No per-user working hours / personal support hours model
- No personal timezone field on user model (only org-level timezone and display component)
- No calendar-to-status sync (calendar events exist but do not affect user status)
- No freebusy API usage (Google Calendar client uses events API, not freebusy)
- No automatic status toggling based on schedule (only manual toggle + timed status with expiry)
- No "meeting in progress" busy indicator from calendar

### Key Files

| File | Purpose |
|---|---|
| `backend/go/src/pylon/person/users/usertypes/usertypes.go` | Status enum, UserSettings struct, ExternalUserMetadata |
| `backend/go/src/pylon/models/user.go` | User model with Status, StatusUntilTime |
| `backend/go/src/pylon/models/external_user.go` | OAuth token storage for calendar integrations |
| `backend/go/src/pylon/graphql/graph/schema.user.graphqls` | SetUserStatus mutation, status fields |
| `backend/go/src/pylon/graphql/graph/schema.user.resolvers.go` | SetUserStatus resolver with issue reassignment |
| `backend/go/src/pylon/person/users/userstatusdetector/user_status_detector.go` | Background poller for timed status expiry |
| `backend/go/src/pylon/externalsystem/calendar/googlecalendar/client.go` | Google Calendar client (readonly events) |
| `backend/go/src/pylon/externalsystem/calendar/outlookcalendar/client.go` | Outlook Calendar client |
| `backend/go/src/pylon/triggers/actionexecutor/executor.go` | Assignment routing with busy status skipping |
| `backend/go/src/pylon/core/eventlog/eventlogmetadata/issue.go` | Skip reason constants for assignment logging |
| `frontend/src/pages/app/settings/support-hours/` | Org-level support hours UI |
| `frontend/src/common/components/timezone-selector/TimezoneSelector.tsx` | Timezone selector component |

### Feature Flags (Status/Calendar-related)

No existing feature flags specifically for personal hours or calendar status sync were found. The feature would need a new feature flag.

---

## Gap Analysis

| Feature | Competitors | Pylon | Gap |
|---|---|---|---|
| Manual status toggle (Active/Away/OOO) | ✅ All platforms | ✅ SetUserStatus mutation with UI | No gap |
| Timed status (auto-revert) | ⚠️ Some (limited) | ✅ StatusUntilTime with background poller | No gap — Pylon is ahead here |
| Issue reassignment on status change | ⚠️ Some (Intercom, Front, Freshdesk) | ✅ Built into SetUserStatus mutation | No gap |
| Status affects assignment routing | ✅ All major platforms | ✅ OnlyAssignIfActive with skip reasons | No gap |
| Per-user working hours | ✅ HubSpot (all plans) | ❌ Not built | **Critical gap vs. HubSpot** |
| Per-user timezone (drives routing) | ✅ HubSpot | ❌ Display component exists, not on user model | Gap — timezone selector exists but not stored per-user |
| Auto Available/Away from hours | ✅ HubSpot, Front, Freshdesk | ❌ Not built | Gap — need scheduled status toggling |
| Google Calendar busy sync | ❌ No platform has this | ❌ Not built | **White space opportunity** — no one does this |
| Outlook Calendar busy sync | ❌ No platform has this | ❌ Not built | **White space opportunity** |
| Shift management (group-level) | ✅ Salesforce, Front, Freshdesk (Enterprise) | ❌ Not built | Gap — but lower priority than per-user hours |
| Idle detection / auto-away | ✅ Salesforce, Zendesk, Intercom | ❌ Not built | Gap — safety net for forgotten status |
| Custom away reasons | ✅ Salesforce, Zendesk, Intercom | ❌ Not built | Nice-to-have |
| Org-level support hours | ✅ All | ✅ SupportHours UI exists | No gap |

### Opportunities

1. **Calendar busy sync is a true differentiator.** No support platform reads Google/Outlook calendar to set agent availability. Pylon already has the calendar OAuth tokens and event subscriptions — adding freebusy checking or event-based status sync would be a unique capability.
2. **Per-user working hours match HubSpot's model.** HubSpot offers this on all plans. Adding per-user timezone + working hours with automatic Available/Away toggling would close the gap with HubSpot and surpass Zendesk, Intercom, and Help Scout.
3. **Microsoft Graph API advantage.** Unlike Google, Microsoft's API exposes working hours. For Outlook Calendar users, Pylon could import working hours automatically — a capability no competitor offers.
4. **Existing infrastructure covers ~70% of the work.** User status system, calendar integrations with OAuth, assignment routing with busy detection, timed status with background poller, and timezone selector component all exist. The main work is: (a) new per-user hours model, (b) calendar-to-status sync worker, (c) personal settings UI.
5. **Org-level support hours UI is a foundation.** The existing SupportHours page pattern can be adapted for per-user hours on the personal settings page.

### Risk: Google Calendar API Scope

Current Google Calendar scopes are `CalendarEventsReadonlyScope` and `CalendarReadonlyScope`. The freebusy API requires `calendar.readonly` or `calendar.freebusy` scope — `CalendarReadonlyScope` should already cover freebusy access, meaning no scope changes or re-authentication should be needed.

---

## Customer Feedback

**Status: Pending — Pylon MCP server needs authentication**

The Pylon MCP server at `https://mcp.usepylon.com/` is configured but requires authentication before customer conversations can be queried. Once authenticated, search for conversations containing:
- "busy status" / "availability" / "away"
- "working hours" / "support hours" / "office hours"
- "calendar" / "google calendar" / "meeting"
- "timezone" / "time zone"
- "schedule" / "shifts"
- "auto-away" / "automatically away"
- "round robin" / "assignment" + "busy"

**To authenticate:** Reconfigure MCP with an API key or OAuth token.

---

## Next Steps

- [ ] **Authenticate Pylon MCP** and gather customer feedback from conversations
- [ ] Validate priority: per-user working hours vs. calendar busy sync (which first?)
- [ ] Design per-user working hours data model (new fields on User or UserSettings)
- [ ] Design calendar-to-status sync worker (polling interval, freebusy vs. event-based)
- [ ] Decide: should Outlook integration import working hours from Microsoft Graph API?
- [ ] Decide: idle detection as a safety net (future scope or V1?)
- [ ] Decide: shift management for teams (future scope or V1?)
- [ ] Personal settings UI wireframes (timezone, working hours, calendar sync toggle)
- [ ] Draft PRD with requirements
