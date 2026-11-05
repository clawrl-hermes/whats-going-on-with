# Frontend content contract

The site reads a strict subset of the wiki repo. Migrate one topic at a time and let the user review before touching the next.

## Allowlist

Published paths only:

```
<topic>/overview.md
<topic>/updates/YYYY-MM-DD.md
<topic>/articles/YYYY-qN.md
<topic>/entities/<slug>.md
<topic>/concepts/<slug>.md
<topic>/sources.md
<topic>/timeline/<any-name>.md   (exactly one file)
```

Never published: `Watch Reports/`, `raw/`, `log.md`, `index.md`, `domain-notes.md`, `priority-sources.md`, `SCHEMA.md`, `watch-reports-summary.md`, `_config.yaml`, `topic-watcher-skill/`, scripts. Do not rewrite these for the site — only update wikilinks that would otherwise break after a rename.

## Per-file requirements

**overview.md** (existence = topic is published). Frontmatter: `title`, `tagline`, `region`, `started`; optional `tone: 1-7`. Body: 1-3 markdown paragraphs. Write it by hand; the agent does not regenerate it.

**updates/YYYY-MM-DD.md** — no frontmatter, no title. Only bullets of the form `- **Headline** — body` on one line. The filename date is the publish date; a future date is scheduled/hidden until that day (UTC).

**articles/YYYY-qN.md** — frontmatter `title`, `summary`, `date`; body starts at `##` (site renders the title).

**entities/**, **concepts/** — frontmatter `title`, `summary` (one sentence), optional `role` (entities), optional `facts:` map, optional `weight:` (lower first). Keep the H1 only if it exactly matches `title`; the site drops a matching leading H1.

**sources.md** — five columns, one leading pipe per row:

```
| # | Publication | Title | Date | Summary |
|---|---|---|---|---|
| 189 | OC Media | [Headline](https://...) | 2026-10-16 | One to three sentences. |
```

`Publication` is the clean outlet name; `Date` is `YYYY-MM-DD`, `YYYY-MM`, or empty.

**timeline/*.md** — one heading per year (`## 2026`). Under it, each month or season is a parent bullet (`- **June:**`, `- **Fall:**`, optionally `(planned)`), and every event is a two-space-indented sub-bullet beneath it. A top-level bullet that is not a month/season label is a year-level event. No day labels, no `###`, no year ranges, no `(continued)`, no prose paragraphs.

## Migration procedure (per topic)

1. **Inventory.** `find <topic> -type f | sort`; read `sources.md`, the timeline, and every entity/concept head. Compare against the contract and note counts before editing.
2. **Rename files** in `entities/`, `concepts/`, `updates/`, `articles/` to `[a-z0-9-]+.md` with `git mv` so history follows. Use ASCII transliteration (`Erdoğan` → `erdogan`).
3. **Update wikilinks** in `index.md` to the new filenames using aliases: `[[nikol-pashinyan|Nikol Pashinyan]]`. Unaliased links to renamed files break in Obsidian; the site renders wikilinks as plain text anyway.
4. **Add frontmatter** to every entity/concept page. Derive `role` from an existing `**Role:**` line when present. Put a blank line between the closing `---` and the H1.
5. **Normalize sources.md** (see recipes below). Verify every row has exactly five cells afterwards.
6. **Fix the timeline** to the heading/label rules; strip stray `|-` bullets.
7. **Write overview.md** with `started` taken from `_config.yaml` `created`.
8. **Create `updates/` and `articles/`** empty when asked. Empty directories are invisible to git — they exist on disk but will not appear in a commit until they contain a file. Do not add `.gitkeep` unless asked for a placeholder.
9. **Validate** (see checker below), report the counts, and stop. Leave changes uncommitted unless the user asks for a commit — they want to run the frontend check first.

## Sources normalization recipes

Rows are routinely prefixed with `||` or `|||` by a historical append bug. Parse by stripping all edge pipes, then splitting:

```python
parts = [x.strip() for x in line.strip("|").split("|")]
```

This tolerates any number of leading pipes. Assert `len(parts) == 4` (old) or `5` (new) before rebuilding; a summary containing a literal `|` will otherwise shift columns silently.

Extract the outlet from the title prefix `Outlet: Headline`, then strip it from the displayed title. Normalize variants: `RFERL` → `RFE/RL`, cross-posts (`OC Media/Mirror-Spectator`, `X (via Y)`) → the first/primary outlet.

Date conversion: `Mon D, YYYY` → `YYYY-MM-DD`; `Month YYYY` → `YYYY-MM`; ranges (`Jul/Aug 2026`, `Sep-Oct 2026`, `Sep 23-25, 2026`) → the first month or first day; `Late/Early/Mid Month YYYY` → `YYYY-MM`. Leave anything unparseable empty rather than guessing.

When appending new rows later, write exactly one leading pipe and the five-column shape — the bug is created at append time, not by the reader.

## Validation checker

Run a stdlib-only pass over the published paths (the sandbox `execute_code` interpreter may lack PyYAML — parse frontmatter with a regex instead of importing it):

- filenames match `^[a-z0-9-]+\.md$`
- every entity/concept has `title` + `summary`; H1 equals `title` when present
- `sources.md` header contains `Publication`; every row has 5 cells; date matches `^\d{4}-\d{2}(-\d{2})?$|^$`; publication non-empty; no row starts `||`
- exactly one timeline file; no `###`, no `(continued)`, no `|-`
- no `|- ` or `||` in any published file (table separator rows `|---|` are legitimate)

## Timeline editorial pass

Format normalization and content condensation are separate passes. Run this one only when the user says the timeline is too granular, too long, or asks what is really timeline-worthy.

1. **Read the whole year**, not just the visible bullets, and put every entry in true chronological order — existing timelines are often out of order because entries were appended as sources arrived.
2. **Select for the arc, not for completeness.** Keep what a new reader needs to understand how the situation unfolded: elections and leadership changes, agreements signed or blocked, major military/security shifts, coercive economic moves (sanctions, energy cutoffs, trade bans), and the diplomatic meetings that changed the trajectory. Cut commentary, think-tank reactions, ceremonial visits, exercises with no policy consequence, and announcements later superseded by a bigger event.
3. **Group by month or season.** Each month/season is a parent bullet, and every surviving event is its own two-space-indented sub-bullet. Do not merge separate events into one sentence to keep the bullet count down — the nested list is what makes the month readable at a glance. A year in progress is roughly six parents.
4. **Month or season only.** Never a day label; fold the day into the sub-bullet text only if the exact date changes the meaning. An event spanning months goes under the month it started. Omit months with nothing that survived selection.
5. **Check for missing recent months.** Timelines routinely lag the source log. Compare the timeline's last entry against `sources.md` and `domain-notes.md`; if recent months are absent, add the high-signal events from existing wiki material and tell the user you did, so they can veto the addition.
6. **Do not duplicate one event across months.** An announcement and the later first shipment/implementation are usually one sub-bullet, not two.
7. **Validate:** every month/season parent matches `^- \*\*(Month|Season)( \(planned\))?:\*\*$`, every event under it starts with exactly two spaces and `- `, parents ascend chronologically, and no day-number labels remain.

## Generating updates and articles

- **Update file:** take the most recent successful weekly monitor notification (`~/.hermes/cron/output/<job_id>/YYYY-MM-DD_*.md`, the `## Response` section), reduce it to 3-6 bullets of the form `- **Headline** — body`, and name the file for that run's date. No frontmatter and no title. If the newest runs failed, use the last run with a real response and tell the user the date you used.
- **Backfilling updates:** enumerate `~/.hermes/cron/output/<job_id>/*.md` in date order and skip any file whose first line contains `(FAILED)` — those have no `## Response`. Parse the `Key Themes This Week` section when present (the heading has appeared as `##`, `###`, and bold text in different runs). Older runs have no themes section and must be condensed from their source tables or prose summaries. One file per successful run, named for the run date; leave failed runs without a file. Reconcile source ranges with git (`git show <commit>:<topic>/sources.md`) rather than trusting the old log, which drifts and does not chain.
- **Quarterly article:** frontmatter `title`, `summary`, `date`; body begins at `##`. Cover only that quarter's developments. Before finishing, grep the draft for later-quarter names, dates, and events and remove them when the user asks for a period-limited piece.
- Both are editorial distillations: prefer the structural consequence over the announcement, and do not introduce facts that are absent from `sources.md` or the timeline.

## Pitfalls

- **Frontmatter replaces body metadata, it does not accompany it.** After deriving `role` and `facts` from `**Role:**`/`**Party:**` lines, delete those lines from the body. The site renders the frontmatter fields, so leaving the old lines shows the same value twice; a frontend check will flag each one.
- **Contract changes are code changes.** When the agreed structure changes (e.g. timeline sub-bullets), update `/root/wiki/content-contract.md` and commit it with the content. The build validates against the written contract; a stale copy silently contradicts the files.
- **Don't trust `git status` shorthand for "staged".** Check `git diff --cached --stat` first; work described as staged is often only in the working tree.
- **Split unrelated changes into separate commits.** A structural migration and a pending weekly source update are different commits; stage everything, `git reset` the unrelated paths, commit, then commit the rest.
- **`git mv` before editing frontmatter** keeps rename detection and avoids delete+add noise in the diff.
- **Format migration does not touch timeline content.** When standardizing a topic for the contract, only headings, labels, and stray pipes change — leave the events themselves for the separate editorial pass the user requests explicitly. Do not combine a migration commit and a timeline rewrite commit.
- **Timeline history is preserved; log history is policy.** Keep timeline entries about retired outputs or past events — they are records. In `log.md`, delete entries for a retired output entirely when the user asks for a concise action log; do not carry report metadata forward.
