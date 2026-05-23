# Journal project guide

Definitions, roadmap, and templates for this project. **Not** your life story — your content lives in other files. When you (or the universe) need structure, start here.

---

## What this project is

A journal to record days, past context, thoughts, dreams, and desires — and to make sense of who you are and where you are going (literally and figuratively). Long-form reflection is welcome. Format can be a **discussion between you and the universe** (AI as voice of the universe when you want it).

---

## Roadmap — how the project gets built

Work in whatever order fits; this is the intended build-out.

| Phase | What to create | Purpose |
|-------|----------------|---------|
| **1** | `thepast.md` | Skeleton of events, places, what mattered — fill in over time |
| **2** | Deepen one line or era from `thepast.md` | Thoughts, feelings, meaning on a single memory or period |
| **3** | `present/` dated entries (optional folder) | Ongoing “now” — where you are day to day |
| **4** | `past/` backfilled memories (optional folder) | Episodes you remember while writing present or map |
| **5** | `universe/` dialogue sessions (optional folder) | Big questions — you and the universe |
| **6** | `themes/` (optional folder) | By topic (family, place, work, desires) when timeline is not enough |

You do not need every phase. Phase 1 is your current starting point.

---

## File map

| File / folder | Role | Status |
|---------------|------|--------|
| `guide.md` | This file — definitions, roadmap, templates | Active |
| `thepast.md` | Events, places, what mattered; skeleton to deepen | Active |
| `present/` | Dated present entries | Not started |
| `past/` | Backfilled memories | Not started |
| `universe/` | Dialogue sessions | Not started |
| `themes/` | Thematic deep dives | Not started |

Update the **Status** column as you add files.

---

## Field definitions

Use these labels across templates (skip any section that has nothing to say).

| Field | Meaning |
|-------|---------|
| **Events** | What happened — facts, places, people, dates when known |
| **Thoughts** | What you believed, feared, hoped, or argued with yourself about |
| **Feelings** | What it felt like in body and mood, not the polished version |
| **Dreams & desires** | What you wanted then, want now, what still pulls you |
| **Meaning** | What it meant then vs. what you think it means now |

---

## Templates

Reference by name: *“Use the `thepast-entry` template”* or *“Use `universe-session`.”*

### `thepast-entry`

One item in `thepast.md` — event plus why it mattered (when you have more than a bullet).

```markdown
### [approx year or age] — [short title]

**What happened:**
-

**Why it mattered to me:**
-
```

---

### `thepast-era`

A decade or life chapter in `thepast.md` — bullets only, no pressure to polish.

```markdown
## [Era name] — [rough years]

-
-
-
```

---

### `present-entry`

Today (or this week) — literal and figurative place.

```markdown
## [YYYY-MM-DD]

**Literally (where):**


**Figuratively (direction):**


**Events:**


**Thoughts:**


**Feelings:**


**Dreams & desires:**
```

---

### `memory-backfill`

A past episode when it surfaces — expand from a single line in `thepast.md`.

```markdown
### Memory — [approx date or age] — [short title]

**What happened:**


**What I thought then:**


**What I feel about it now:**


**What it might mean for who I am / where I am going:**
```

---

### `universe-session`

You ask; the universe answers; you can continue the thread.

```markdown
## Universe — [YYYY-MM-DD]

**You:**


**Universe:**


**You:** *(optional follow-up)*


**Universe:**
```

---

## Ways to organize content (reference)

You can mix these; most people use a **hybrid** (`thepast.md` first, present ongoing, backfill when triggered).

1. **Present-first** — write now; past when memory surfaces  
2. **Outline-first** — skeleton then deepen *(your starting approach)*  
3. **Thematic** — by what matters (family, place, desires), not by year  
4. **Chapters / eras** — named periods, subfiles per chapter  
5. **Anchor objects** — one photo, song, place, dream per entry  
6. **Dialogue** — universe sessions; past enters when the question needs it  
7. **Dual timeline** — outer facts vs. inner beliefs, linked when you can  

**Practical hybrid:** maintain `thepast.md` → daily or weekly `present-entry` → `memory-backfill` or `universe-session` when something pulls you.

---

## Working agreements

- Dates can be approximate; truth of feeling matters more than precision.  
- Contradictions are allowed — you can change your mind about the past.  
- Long entries are welcome; silence is also allowed.  
- Not for an audience unless you decide otherwise later.  

### Day files (`days/*.md`) — no sticky headers

**Do not use `##` or `###` section headings in day conversation logs.** They trigger Cursor/VS Code sticky scroll (headers pinned at the top of the editor) and the user has disabled that repeatedly.

**Use instead:**

- One top title only: `# Journal — [date]`
- Separate exchanges with `---` on its own line
- Speaker labels: `**You:**` and `**Assistant:**` only (no `### Session start`, `### Rabbit Ears`, etc.)

---

## For AI / “the universe”

### Top 3 rules (read these first)

1. **Do not regurgitate what the user said.** They already know what they said. Do not summarize their message back in list or scene form. Respond with new thought, question, or connection — not a replay.  
   - **Wrong:** “You were not only listing purchases; you were running a full scene — the house handled, the car, travel, banjo, Spanish, painting, money arriving…”  
   - **Right:** “That practice is the ease-and-bank-balance version, not the scared version from the 18th — which one shows up when you are working on the launch?”  
   - **Do not log meta-instructions about AI behavior in `days/*.md`** (e.g. “add this rule to guide”) unless the user asks. Those belong in `guide.md` only, not in the day conversation.

2. **No `##` / `###` headings in `days/*.md`.** See **Day files — no sticky headers** under Working agreements. One `#` title, then `---` and `**You:**` / `**Assistant:**` only.

3. **Write in full sentences.** No telegraphic fragments. One main thread per reply unless the user asks you to tie threads together.

---

When asked to help write in this project:

1. Read `guide.md` for structure and template names — especially **Top 3 rules** above.  
2. Use the template the user names, or ask which file and template apply.  
3. Put personal content only in the user’s content files (e.g. `thepast.md`), not in `guide.md`.  
4. **Day logs:** follow **Day files — no sticky headers** and **Top 3 rules**.  
