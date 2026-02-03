# Technical Documentation Generation Prompt

Use this prompt when generating internal technical documentation from codebase analysis.

---

## CRITICAL RULES

### 1. Only document what's implemented
- Do NOT list features that aren't working
- Do NOT include "Not implemented" rows
- If it doesn't work, it doesn't exist in the doc
- Constants and type definitions are NOT features

### 2. Verify implementations, not definitions
- Type definitions, structs, and constants do NOT prove something works
- You must trace the actual execution path to verify functionality
- Look for: TODO comments, empty array initializations, error returns, stubbed functions
- If you find any of these → do not include the feature

### 3. For each feature/capability, ask:
- Where is the entry point?
- What functions are actually called?
- Is there real logic, or just a type/constant defined?
- Does the execution path complete, or does it error out?

### 4. Data sources checklist
- Find where data is fetched (look for DB queries, API calls)
- If a field exists in a struct but no query populates it → exclude
- If there's a TODO comment → exclude

### 5. Configuration options checklist
- Find where the option is actually handled (switch statements, if conditions)
- If a constant exists but no code handles it → exclude
- If handling returns an error → exclude

### 6. Documentation format
- Use tables for structured information
- Include file:line references for every claim
- No code blocks - just references
- Keep it scannable

---

## OUTPUT TEMPLATE

```markdown
# [Feature Name] - Technical Documentation

*All statements verified against actual implementation.*

---

## Overview
[1-2 sentences. Entry point reference.]

---

## [Core Functionality - e.g., Data Sources]
| Item | Reference |
|------|-----------|
| [Name] | `file.go:line` |

---

## [Processing/Pipeline]
**Stage N:** [Description] (`file.go:line`)
| Setting | Value | Reference |
|---------|-------|-----------|
| [Name] | [Value] | `file.go:line` |

---

## Configuration
**[Category]** (`file.go:lines`)
| Option | Value | Reference |
|--------|-------|-----------|
| [Name] | [Value] | `file.go:line` |

---

## Database Tables
| Table | Model | Reference |
|-------|-------|-----------|
| [name] | [Struct] | `models/file.go:line` |

---

## Execution Flow
1. [Step] — `file.go:line`
2. [Step] — `file.go:line`

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
