# PRD Research: $ARGUMENTS

Research the feature "$ARGUMENTS" to build an informed baseline for PRD writing.

## Phase 1: Competitive Research

Search competitors for how they implement this feature:
- Salesforce
- Zendesk
- Intercom
- HubSpot (if relevant)

For each competitor, find:
- What they call this feature
- How it works (high-level)
- Key capabilities and limitations
- Pricing tier (if visible)

Identify common patterns:
- What's table stakes (everyone has it)
- What's differentiated
- Common use cases

## Phase 2: Codebase Research

Search the Pylon codebase at /Users/isaacgueu/Downloads/app-main for existing implementation:

1. **Data model**: Search for related models, database tables, structs
2. **Current capabilities**: What's already built?
3. **Configuration**: How is it configured today?
4. **Key files**: List the main files with line references

Look in:
- `backend/go/src/pylon/models/`
- `backend/go/src/pylon/graphql/graph/`
- Feature-specific directories
- Use grep/glob to find related code

## Phase 3: Gap Analysis

Compare competitors vs current implementation:
- What do we have that others don't?
- What are we missing that's table stakes?
- What are we missing that's a differentiator?

## Output Format

```markdown
## [Feature Name]: PRD Research Baseline

### Summary
[2-3 sentences on what this feature is and why it matters]

---

### Competitive Analysis

#### Salesforce
- **Feature name:**
- **How it works:**
- **Key capabilities:**
- **Limitations:**
- **Sources:** [links]

#### Zendesk
[same structure]

#### Intercom
[same structure]

#### HubSpot
[same structure]

### Common Patterns
| Feature | Salesforce | Zendesk | Intercom | HubSpot |
|---------|------------|---------|----------|---------|
| [capability] | ✅/❌ | ✅/❌ | ✅/❌ | ✅/❌ |

---

### Current Pylon Implementation

#### Data Model
| Table/Struct | Purpose | Reference |
|--------------|---------|-----------|
| [name] | [what it does] | `file.go:line` |

#### Current Capabilities
- [What's already built]

#### Key Files
| File | Purpose |
|------|---------|
| [path] | [description] |

---

### Gap Analysis

| Feature | Competitors | Pylon | Gap |
|---------|-------------|-------|-----|
| [name] | ✅ All have it | ✅/❌ | [description] |

### Opportunities
- [Market gaps identified]
- [Differentiation possibilities]
- [User expectations from competitor migrations]

---

### Customer Feedback
[To be filled in from Pylon conversations - search for "$ARGUMENTS" related tickets]

---

### Next Steps
1. [ ] Gather customer feedback from Pylon conversations
2. [ ] Validate gaps with internal stakeholders
3. [ ] Draft PRD with requirements
```

Include source links for all competitive claims.
Include file:line references for all codebase claims.
