# Content contract

**Status: draft for review.** Last updated 2026-11-05: timeline events are now sub-bullets under month/season parents. This is what the site reads from the wiki repo. The build checks every file against it and reports the exact file and line that is wrong.

Principles:

- **The site shows what the files say.** It does not repair, prune or reinterpret them. If a file follows the contract, it renders as intended.
- **Allowlist.** Only the paths below are read. Everything else is never published: `Watch Reports/`, `raw/`, `log.md`, `index.md`, `domain-notes.md`, `priority-sources.md`, `SCHEMA.md`, `watch-reports-summary.md`, `_config.yaml`, `topic-watcher-skill/` and the scripts.
- **The folder name is the URL slug.** `armenia-azerbaijan/` becomes `/topics/armenia-azerbaijan`.

## Layout

```
<topic>/
  overview.md                 a topic is published if, and only if, this file exists
  updates/2026-10-18.md       one file per update; the filename is the publish date
  articles/2026-q3.md         one file per quarterly article
  entities/nikol-pashinyan.md shown on the site as "Actors"
  concepts/tripp.md           shown on the site as "Explainers"
  sources.md
  timeline/<any name>.md      exactly one file
```

File names in `entities/`, `concepts/`, `updates/` and `articles/` use only `a-z`, `0-9` and `-`. No spaces, capitals, apostrophes or accents. The display name comes from `title`, never from the file name.

## `overview.md`

New file. Written once, edited by hand when needed; the agent does not rewrite it.

```md
---
title: Armenia-Azerbaijan Relations
tagline: One line for topic cards.
region: South Caucasus
started: 2026-06-09
---

One to three paragraphs describing what the topic covers and why it matters. Markdown.
```

`title` reads as "What's going on with *Armenia-Azerbaijan Relations*". `started` is when tracking began. An optional `tone: 1` to `7` pins the topic's colour; otherwise the site picks one.

## `updates/YYYY-MM-DD.md`

New. No frontmatter and no title: only the bullets, in the shape from the spec.

```md
- **Pashinyan locks in 2031 peace target** — Explicit deadline for treaty signing/ratification, paired with a bold enclave/exclave territory exchange proposal.
- **Russia-Armenia railway concession showdown** — 3-month working group buys time, but Russia resists transfer while refusing to invest.
```

Each bullet is `- **Headline** — body` (bold headline, em dash, body on one line). The filename date is the publish date and is shown as such. A date in the future is a scheduled update: it stays hidden until that day (UTC).

## `articles/YYYY-qN.md`

New. One per quarter, e.g. `2026-q3.md`.

```md
---
title: Peace without a signature
summary: One or two sentences for cards and link previews.
date: 2026-10-19
---

## The short version

Markdown body. Start at `##`: the site renders the title itself.
```

## `entities/*.md` and `concepts/*.md`

Existing pages, plus frontmatter. Sri Lanka's `SCHEMA.md` already asks for frontmatter on every page; the site needs these fields:

```md
---
title: Nikol Pashinyan
summary: One sentence for the card.
role: Prime Minister of Armenia (since 2018)   # optional, entities only
facts:                                         # optional
  Party: Civil Contract
weight: 1                                      # optional, lower comes first; default is alphabetical
---

# Nikol Pashinyan        <- optional; the site drops a leading H1 that matches the title

Body in markdown.
```

Rendering rules: `[[wikilinks]]` show as plain text; `^[raw/...]` provenance markers are dropped.

## `sources.md`

A table, one source per row, with a new **Publication** column so the site no longer has to guess the outlet from the title.

```md
| # | Publication | Title | Date | Summary |
|---|---|---|---|---|
| 189 | OC Media | [Pashinyan says he aims to sign peace agreement by 2031](https://oc-media.org/...) | 2026-10-16 | One to three sentences. |
```

`Publication` is the clean display name ("RFE/RL", not "RFERL" or "RFERL (via X)"). `Date` is `YYYY-MM-DD`, or `YYYY-MM` when only the month is known, or empty. Rows start with a single `|`.

## `timeline/*.md`

As agreed: **month or season is the lowest unit shown**, and each event is a sub-bullet under its month.

```md
# Timeline: Armenia-Azerbaijan Relations

## 2026
- **June:**
  - Civil Contract wins the parliamentary election with 49.8%.
  - Parliament elects a new speaker.
- **Fall:**
  - Constitutional referendum (planned).

## 2025
- **August:**
  - Background event.
- A year-level event with no month, such as a ceasefire that held all year.
```

- One heading per year: `## 2026`. No ranges, no subtitles, no "(continued)".
- A month or season is a parent bullet: `- **June:**`, `- **Fall:**`, optionally with `(planned)`. Days are not used as labels.
- Each event is a two-space-indented sub-bullet under its month or season. If an event spans months, use the month it started.
- A top-level bullet that is not a month or season label is a year-level event.
- Nothing else under a year heading: no paragraphs and no `###` headings.

## What the build does with problems

- Anything the site would have to leave out or show garbled is an error and fails the build. The previous deploy stays live, and the log names the file and line.
  - an overview.md, update or article that breaks the contract
  - a wiki page whose frontmatter can't be read, or that has no body
  - a source row, or text outside the table, in the wrong format
  - a timeline line in the wrong format, or more than one file in timeline/
  - a stray | in front of a list item
- A problem the content survives is a warning in the build log: a missing title or summary, an unknown frontmatter key, a heading that differs from the title, a month with no events, or a missing sources.md or timeline.
- A topic with no overview.md is not read, so it can be cleaned up without breaking the build.

## What the agent does differently

1. After each weekly run, write `updates/<today>.md` (3 to 6 bullets on what changed since the last update). Commit it with the rest.
2. Once a quarter, write `articles/<year>-q<n>.md`.
3. Append to `sources.md` in the new five-column format, with a clean publication name and an ISO date.
4. Give every new entity and concept page the frontmatter above.
5. Keep timeline entries to the format above.

Everything else (searching, log, index, domain notes) stays as it is.

## Cleanup checklist (audit of the repo on 2026-11-04)

| Area | What needs changing |
|---|---|
| **All topics** | Add `overview.md`. Names exist in `_config.yaml`, but taglines and regions exist nowhere, and four slugs in the config (Georgia, Kazakhstan, China-Southern Africa, Sri Lanka) differ from their folder names. |
| **Stray pipe** | Most rows in `sources.md` start with `\|\|` (Armenia 145, Georgia 80, Kazakhstan 36, China 29, Philippines 25), and 21 wiki pages have `\|- ` bullets. It looks like one agent bug that prepends `\|` to appended lines. Fixing it at the source matters more than repairing the files. |
| **`sources.md`** | Add the Publication column and ISO dates to all seven. Sri Lanka is a numbered list and needs converting to a table. |
| **File names** | Armenia: 9 files (spaces, capitals, `Erdoğan`). Bolivia: 7 (spaces, apostrophes, `(MAS)`). Philippines: 6 (mixed case). China, Georgia, Kazakhstan and Sri Lanka are already fine. |
| **Frontmatter** | 50 of 55 entity and concept pages have none. Sri Lanka's 5 have it but no `summary`. A one-off agent pass can add `title` and `summary` to all of them. |
| **Armenia timeline** | Already compliant. |
| **Bolivia timeline** | Labels like `Early May`, `Late June - Early July`: use the month. |
| **China-Southern Africa timeline** | Labels like `June 2026`, `July 28, 2026`, `2025` under year headings: use `June`, `July`, or an unlabelled bullet. |
| **Georgia timeline** | `## 2026 (continued)` heading, and 51 `###` day headings (`### June 8`) with bullets beneath. Those need merging into month-level bullets such as `- **June:** ...`. |
| **Kazakhstan timeline** | Year-range headings (`## 1993–2000s`, `## 2008–2009`, `## 2014–2015`). The 28 unlabelled bullets are fine. |
| **Philippines timeline** | `## 2023–2024` heading, and labels like `Throughout`, `May–October`, `Founding`. |
| **Sri Lanka timeline** | Prose sections under headings like `## 2005 -- Mahinda Rajapaksa Elected President`. Needs rewriting as bullets under `## 2005`. |
