# Prompt: "Feature -> import-ready JSON for a tracker"

<!-- ============================================================= -->
<!-- 🔴🔴🔴  BLOCK ONLY FOR YOU. DELETE IT BEFORE SENDING TO THE AI  🔴🔴🔴 -->
<!-- ============================================================= -->

> ## 🔴 INSTRUCTION FOR YOU (NOT FOR THE AI) - DELETE THIS BLOCK BEFORE SENDING
>
> 1. Fill in **only one block - `🎯 FEATURE DESCRIPTION`** (below).
> 2. Before sending the prompt to the AI, **delete two blocks** marked in red:
>    - this instruction block;
>    - the guiding questions inside `🎯 FEATURE DESCRIPTION` (after you write your description).
> 3. Leave the `⚙️ CONFIG` block in place - the AI reads it. You may change the values, but you do not have to.
> 4. Do not touch anything below `⚙️ CONFIG` - it is the schema and rules for the AI.
> 5. As output, you will get clean JSON -> save it as `.json` -> upload it with the **"↑ Upload full JSON"** button.

<!-- 🔴🔴🔴  END OF BLOCK FOR YOU - DELETE EVERYTHING ABOVE THIS LINE  🔴🔴🔴 -->
<!-- ============================================================= -->

---

## 🎯 FEATURE DESCRIPTION  <- *(fill in only this)*

```
<here - in your own words - describe the feature. Bullet points are fine.>
```

<!-- ============================================================= -->
<!-- 🔴🔴🔴  GUIDING QUESTIONS. DELETE THEM AFTER YOU WRITE THE DESCRIPTION  🔴🔴🔴 -->

> 🔴 **Prompts for inspiration - delete this block after filling in the description.**
> You do not have to answer everything, but the more you answer, the more accurate the JSON will be:
- [ ] What is the feature and **what problem** does it solve? Why does the business and the user need it?
- [ ] **Who** uses it - all roles, including operators, compliance/admins, and the system role "Platform" (backend)?
- [ ] What are the **main end-to-end scenarios**? What are the error scenarios and edge cases?
- [ ] What is required for **MVP**, and what can be postponed to **R1 / R2**?
- [ ] Are there any **integrations**: external services, APIs, payment gateways, email/SMS services?
- [ ] What are the **constraints**: legal/regulatory (law numbers), security, performance, deadlines?
- [ ] What are the **open questions and assumptions** (later they can be conveniently moved to `deps`)?

<!-- 🔴🔴🔴  END OF GUIDING QUESTIONS - DELETE THE ENTIRE BLOCK ABOVE  🔴🔴🔴 -->
<!-- ============================================================= -->

---

## ⚙️ CONFIG  *(leave for the AI; values can be edited)*

```
First sprint start date: the nearest Monday - the first business day
   of the nearest work week. Calculate from today's date: if today
   is Monday - use today; otherwise - use the next nearest Monday.
Sprint length: 14 days (2 weeks), start - Monday, finish - Sunday
Sprint capacity (SP): 30
1 SP = 8 hours
Number of sprints: calculate automatically - as many as needed for the feature scope
Release-to-sprint mapping: MVP -> first sprints, R1 -> next sprints, R2 -> last sprints
Story ID prefix: US-
```

---

## 🧠 WHAT YOU MUST DO

You are a senior product analyst and Scrum Master. Based on the "FEATURE DESCRIPTION" block, perform a complete analysis and plan the work strictly step by step:

1. **Feature analysis.** Break down the goal, business and user value, key scenarios, edge cases, dependencies, and risks (including regulatory/legal risks, if applicable).
2. **Roles and personas.** Identify all roles affected by the feature: end users, operators, compliance/admins, and the system role **"Platform"** (backend/system requirements). For each one, provide a short description and a color (hex).
3. **Activities (journey stages).** Group the work into user journey stages / functional blocks. Assign each activity a short code (`A1`, `A2`, `B1`, `O1`, `C1`...) and a human-readable name.
4. **INVEST user stories.** For each story, formulate the three parts separately: **role** (as a...), **action** (I want to...), **value** (so that...). Add 2-5 clear **acceptance criteria**.
5. **Estimation (Story Points).** Estimate each story using **only these values: 1, 2, 3, 5, 8, 13, 20, 40, 100**. Whenever possible, split stories larger than 13 SP into smaller ones.
6. **Priority.** Assign `P0` (critical/MVP blocker), `P1` (important), or `P2` (nice to have).
7. **Dependencies.** In `deps`, specify IDs of other stories (`US-XX`) or external references (laws/standards, external services, open questions - for example `Email service`, `Q1`).
8. **Sprint and timeline planning.** Distribute stories across sprints so that:
   - total SP in one sprint **does not exceed that sprint's capacity**;
   - dependencies come **before** the stories that depend on them;
   - `P0` stories are placed in the earliest sprints;
   - each story's `release` matches the release of its sprint.
   Generate sprints (`S1`, `S2`, ...) with real dates, counting from the start date in increments equal to the sprint length.
9. **Milestones and legal track** (if applicable). Add key milestones (dates + label) and legal/preparatory tasks to `legal`.

---

## 📐 OUTPUT JSON SCHEMA (follow strictly)

> The examples below are **neutral format examples** (not tied to any domain). Substitute your own values based on the feature. Dates are examples only; calculate actual dates from the "Start date" in CONFIG.

Top level - exactly one object with exactly these keys:

```jsonc
{
  "stories":          [ /* array of stories, see below - REQUIRED */ ],
  "activities":       [ { "code": "A1", "name": "Onboarding" } ],
  "activityOrder":    [ "A1", "A2", "A3", "A4", "A5", "A6" ],   // display order, all codes from activities
  "sprints":          [ { "code": "S1", "start": "2026-06-01", "end": "2026-06-14", "release": "MVP", "capacity": 30 } ],
  "personas":         [
                        { "name": "User",     "desc": "Target end user of the product",      "color": "#0EA5E9" },
                        { "name": "Platform", "desc": "Backend / system requirements",       "color": "#94A3B8" }
                      ],
  "spHours":          8,                                         // hours in 1 SP
  "milestones":       [ { "date": "2026-09-30", "label": "🚀 MVP release" } ],
  "legal":            [ { "code": "L1", "name": "Prepare legal documentation", "start": "2026-06-29", "end": "2026-07-26", "critical": true } ],
  "versions":         [],
  "currentVersionId": null,
  "exportedAt":       "2026-06-01T00:00:00.000Z"                 // generation ISO timestamp
}
```

**Story object (an element of `stories[]`) - neutral format example:**

```jsonc
{
  "id":           "US-04",                              // unique, prefix from config
  "activity":     "A1",                                 // code, must exist in activities[]
  "activityName": "Onboarding",                         // MUST match this activity's name
  "persona":      "User",                               // must match one of personas[].name
  "role":         "new user",                           // "as a ..." part
  "action":       "register by email",                  // "I want to ..." part
  "value":        "quickly start using the product",     // "so that ..." part
  "ac": [                                               // acceptance criteria, 2-5 items
    "The form accepts email and password",
    "Confirmation happens via a link from the email",
    "The profile is created automatically",
    "A successful registration notification is shown"
  ],
  "sp":           8,                                    // one of: 1,2,3,5,8,13,20,40,100
  "sprint":       "S1",                                 // code, must exist in sprints[]
  "release":      "MVP",                                // exactly one of: MVP | R1 | R2
  "priority":     "P0",                                 // exactly one of: P0 | P1 | P2
  "deps":         [],                                   // array of strings: "US-XX" or external references
  "status":       "todo",                               // OPTIONAL: todo | in_progress | done (default: todo)
  "tfsPbi":       []                                    // OPTIONAL: array of strings (PBI numbers)
}
```

---

## ✅ STRICT VALIDATION RULES (check before output)

1. `priority` - only `P0`/`P1`/`P2`. `release` - only `MVP`/`R1`/`R2`. `status` - only `todo`/`in_progress`/`done`.
2. `sp` - only from the set `1,2,3,5,8,13,20,40,100`. No other numbers.
3. Every `story.activity` exists in `activities[]`, and `activityName` is exactly equal to its `name`.
4. Every `story.persona` exists in `personas[]` (`name`).
5. Every `story.sprint` exists in `sprints[]`, and `story.release` equals that sprint's `release`.
6. All codes from `activities[]` are listed in `activityOrder[]` in a logical order.
7. The sum of `sp` for all stories in each sprint is **<=** that sprint's `capacity`.
8. All `id` values are unique; `US-XX` references in `deps` point to stories that actually exist.
9. Dates use the `YYYY-MM-DD` format. Persona `color` values are hex (`#RRGGBB`).
10. `versions: []`, `currentVersionId: null`, and `exportedAt` are a valid ISO timestamp.

---

## 📤 RESPONSE FORMAT

Output **only the JSON object itself** - no markdown fences (` ``` `), no comments, no explanations before or after. The response must be valid JSON that can be saved directly as a `.json` file and imported into the product. The first character of the response must be `{`, and the last character must be `}`.
