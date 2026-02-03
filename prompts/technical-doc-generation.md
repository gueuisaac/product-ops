# Technical Documentation Generation Prompt

Use this prompt when generating internal technical documentation from codebase analysis.

---

## DISCOVERY PROCESS

### Step 1: Find the entry point
- Locate the main function or API endpoint that triggers the feature
- Document the file:line reference

### Step 2: Trace the full execution path
- Follow function calls from entry point to completion
- Map out the complete data flow
- Identify all major steps/stages in the process

### Step 3: Document each stage thoroughly
For each stage in the process, find and document:
- What data comes in
- What processing happens
- What data comes out
- Any aggregation or combination logic (e.g., intermediate → final)

### Step 4: Find all configuration touchpoints
- Filters: What can users filter by? Trace filter application in code
- Custom fields: Are custom fields supported? How are they used?
- Settings: What options affect behavior?

### Step 5: Document the data model
- What database tables are involved?
- How do they relate to each other?
- What's the lifecycle of data (created → updated → used)?

---

## CRITICAL RULES

### 1. Only document what's implemented
- Do NOT list features that aren't working
- If it doesn't work, it doesn't exist in the doc
- Constants and type definitions are NOT features

### 2. Verify implementations, not definitions
- Type definitions, structs, and constants do NOT prove something works
- Trace the actual execution path to verify functionality
- Look for: TODO comments, empty array initializations, error returns
- If you find any of these → do not include the feature

### 3. Be thorough about processes
- Don't just list "what" - explain "how"
- If data is aggregated or combined, document that process
- If there are multiple stages, explain how they connect

### 4. Document filtering and customization
- What filters are available and where are they applied?
- Are custom fields supported? How?
- What can users configure?

---

## OUTPUT TEMPLATE

```markdown
# [Feature Name] - Technical Documentation

*All statements verified against actual implementation.*

---

## Overview
[2-3 sentences explaining what the feature does and how it works at a high level.]

**Entry point:** `file.go:line`

---

## How It Works

### [Stage 1 Name]
[Explain what happens in this stage]

| Input | Output | Reference |
|-------|--------|-----------|
| [what comes in] | [what comes out] | `file.go:line` |

### [Stage 2 Name]
[Explain what happens, especially any aggregation/combination logic]

...continue for each stage...

---

## Data Sources
| Source | Reference |
|--------|-----------|
| [Name] | `file.go:line` |

---

## Filters
| Filter | Applied At | Reference |
|--------|------------|-----------|
| [Name] | [where in the process] | `file.go:line` |

---

## Configuration
| Setting | Value | Reference |
|---------|-------|-----------|
| [Name] | [Value] | `file.go:line` |

---

## Database Tables
| Table | Purpose | Reference |
|-------|---------|-----------|
| [name] | [what it stores] | `models/file.go:line` |

---

## Key Files
| File | Purpose |
|------|---------|
| [path] | [description] |
```

---

## VERIFICATION CHECKLIST

Before including any claim:
- [ ] Found the actual function that does this (not just a type)
- [ ] Traced from entry point to this function
- [ ] Confirmed no TODO/stub/error-return blocking it
- [ ] Have a specific file:line reference
- [ ] The feature actually works end-to-end

Before finalizing the doc:
- [ ] Documented the full process, not just components
- [ ] Explained any aggregation/combination logic
- [ ] Listed all available filters
- [ ] Noted custom field support (or lack thereof)
- [ ] Covered the complete data lifecycle
