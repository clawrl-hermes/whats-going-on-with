# {Topic Name} — Domain Notes

> Recent developments are tracked in `timeline/{slug}-timeline.md` at month/season resolution, with events as sub-bullets. This file records structural context and recurring dynamics, not a chronology — do not add a Key Recent Developments section.

## Wiki Location
- Path: `/root/wiki/{slug}/`
- Repo: `clawrl-hermes/whats-going-on-with` (canonical; the old `kent-iscann/signal-fracture-content` URL redirects here)
- Git auth: credential helper (no gh CLI needed)

## Folder Structure
```
/root/wiki/{slug}/
├── overview.md           (frontmatter + 1-3 paragraphs; published as the topic page)
├── index.md              (source count + last-updated date + page catalog)
├── sources.md            (five-column table: # | Publication | Title | Date | Summary)
├── domain-notes.md       (this file — topic context, search queries, dedup tips)
├── priority-sources.md   (curated high-value outlets)
├── log.md                (action record: counts and pages updated, no source summaries)
├── timeline/
│   └── {slug}-timeline.md  (month/season parent bullets with event sub-bullets)
├── entities/             (frontmatter: title, summary, role, optional facts)
├── concepts/             (frontmatter: title, summary)
├── updates/              (YYYY-MM-DD.md, 3-6 bullets, no frontmatter)
└── articles/             (YYYY-qN.md, quarterly analysis)
```

## Search Queries (canonical)
1. "{query 1}"
2. "{query 2}"
3. "{query 3}"
4. "{query 4}"
5. "{query 5}"

## Key Entities Tracked
| Entity | Role | Key Actors |
|--------|------|------------|

## Key Data Points
- 

## Common Dedup Pitfalls
- 

## High-Signal Source Types
- 

## File Update Checklist (per source added)
1. ✅ `sources.md` — append a five-column row with Publication and ISO date
2. ✅ `timeline/{slug}-timeline.md` — add a sub-bullet under its month/season parent
3. ✅ `entities/<entity>.md` — update if the source mentions a specific actor
4. ✅ `concepts/<concept>.md` — update if the source relates to a tracked concept
5. ✅ `updates/<YYYY-MM-DD>.md` — write the weekly update (3-6 bullets)
6. ✅ `index.md` — increment source count, update date
7. ✅ `log.md` — append counts and pages updated (no per-source lines)