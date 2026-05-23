# Journal

A personal repository for reflection, life context, and ongoing dialogue — written for myself, not an audience. Content is mostly Markdown so it syncs anywhere via git.

## What this is

This project is a journal to record:

- **Days** — thoughts, feelings, and conversations (often with AI as a reflective partner)
- **Past** — events, places, people, and what mattered over time
- **Direction** — who I am now and where I am going, literally and figuratively

Long-form reflection is welcome. Some threads are practical (work, money, projects); others are spiritual or inner life. Contradictions and changes of mind are allowed.

## Start here

| File / folder | Purpose |
|---------------|---------|
| [`guide.md`](guide.md) | Project rules, templates, roadmap, and instructions for AI helpers |
| [`thepast.md`](thepast.md) | Skeleton timeline of life events and eras — deepened over time |
| [`days/`](days/) | Dated conversation logs (e.g. `may21.md`) |
| [`spirit_work/`](spirit_work/) | Dreams, readings, tarot notes, and related spiritual journaling |
| [`moving-forward/`](moving-forward/) | Health, mindset, and “moving forward” writing (separate subproject; see its README) |

**New to the repo?** Read `guide.md` first. For a given day, open or create a file in `days/`.

## How `days/` works

Each day file is a **conversation log**:

- One title: `# Journal — [date]`
- Exchanges separated by `---`
- Speakers: `**You:**` and `**Assistant:**`
- No `##` / `###` section headings in day files (editor sticky-scroll preference)

The assistant logs the thread when asked; personal story stays in these files, not in `guide.md`.

## Optional future structure

`guide.md` describes phases you may add later: `present/`, `past/`, `universe/`, `themes/`. They are not required to use the journal.

## Privacy

This repo is **private personal writing**. Do not publish or share without a deliberate decision to do so. If you use a remote (GitHub, etc.), keep the repository private.

## Editor notes

- Workspace setting: `editor.stickyScroll.enabled` is off in `.vscode/settings.json` for this project.
- AI helpers working in this repo should follow **Top 3 rules** in `guide.md` (no regurgitation, full sentences, day-file formatting).

## Sync

```bash
git clone <your-remote-url>
cd journal
# edit, commit, push as usual
```
