# Content substance guidelines

**Status: draft for review — 2026-11-10.** This file defines *what each published file should say*. Format, filenames and the publish allowlist are defined in `content-contract.md`; update timing and ownership are in `content-update-policy.md`. Where the three overlap, this file wins on substance, the contract wins on format.

The Armenia-Azerbaijan topic is the reference implementation. Its files are cited below as models, not as templates to copy verbatim.

---

## 1. Principles

1. **Actor-first, not event-first.** Every page answers a version of: how does this change the topic? A fact that does not bear on the central conflict, negotiation or system being tracked does not belong on an entity or concept page.
2. **One canonical home per fact.** A fact is stated in full once, then referenced elsewhere in a clause. The map in §10 decides where it lives.
3. **Facts need sources; analysis needs a name.** Reported facts cite a source. Interpretations cite the analyst or outlet that made them ("OC Media called it…", "Modern Diplomacy's base case is…"). The wiki's own synthesis is allowed — but only in an article's argument or the current-situation's open question, and it must read as argument, not as reporting.
4. **Pages speak from their own date.** An update is written for its day; an article for its quarter. Neither may use material published after that date. A static page carries no date, so it must avoid "currently" and "now" where the claim will age badly.
5. **Static pages are reviewed, not appended.** Overview, timeline, entities and concepts are rewritten when the structure of the story changes. Weekly news belongs in updates.

## 2. Voice and length

| File | Purpose | Target length | Model |
|---|---|---|---|
| `overview.md` | Evergreen framing of the topic | 2-3 paragraphs, 120-200 words | Armenia-Azerbaijan |
| `current-situation.md` | Where it stands now | 3-5 sentences + one question + 6-8 watch rows | Armenia-Azerbaijan |
| `updates/YYYY-MM-DD.md` | What changed this week | 3-6 bullets, 25-60 words each | 2026-11-07 |
| `articles/YYYY-qN.md` | Quarterly argument | 900-1,200 words, 15-30 footnotes | 2026-q3 |
| `entities/<slug>.md` | One actor's leverage and limits | 230-350 words | Pashinyan, Aliyev, Iran |
| `concepts/<slug>.md` | One mechanism the reader needs | 240-420 words | TRIPP, Border Delimitation |
| `timeline/<slug>-timeline.md` | Defining events only | 40-100 lines | Armenia-Azerbaijan |
| `sources.md` | The evidence base | One row per source | Armenia-Azerbaijan |

Voice: plain declarative prose, active verbs, no throat-clearing. A reader should be able to stop after any paragraph and still know what it established. Avoid adjectives that do the work of evidence ("dramatic", "historic", "unprecedented") unless a source used them and is named.

---

## 3. `overview.md`

**Purpose:** tell a first-time reader what the topic is, why it matters, and what the coverage follows. It is the only page that should still make sense in a year.

**Must contain**
- Frontmatter: `title`, `tagline` (one line for a card), `region`, `started`.
- Paragraph 1: the subject and the tension. Name the central negotiation, conflict or system.
- Paragraph 2: the through-line — the one dynamic that explains most developments.
- Paragraph 3: what coverage extends to (the adjacent files: corridors, external actors, domestic politics).

**Must not contain**
- Dates of recent events, names of this month's decisions, or anything that will be stale in a quarter.
- Lists of actors or files; those are the index's job.
- Predictions.

**Model:** Armenia-Azerbaijan's overview states the move from war to a signed peace, the rebalancing away from Russia, and the corridor competition — three paragraphs, no news.

**Review trigger:** the topic's central question changes (war ends, treaty signed, government falls). Not on a schedule.

---

## 4. `current-situation.md`

**Purpose:** answer "where does this stand right now?" in under a minute.

**Must contain**
- Frontmatter: `title: Current Situation`, `last_updated` (the revision date, not the newest source's date).
- Three to five sentences: the state of the central negotiation, each side's position, and the most recent decision that changed the picture.
- `## The Open Question` — exactly one sentence naming what the next month will settle.
- `## What to Watch For` — a table, `| Date | What to Watch | Why It Matters |`, covering roughly the next four weeks. Every row carries a date: an exact day, a month, or a bounded phrase ("By end-November"). Nothing beyond the horizon.

**Must not contain**
- Chronology or background. If a sentence could have been written three months ago, it does not belong.
- Analysis without attribution, except the open question, which is explicitly the wiki's framing.
- More than one open question, or a question that is really two questions.
- Rows without dates, or speculative rows with no scheduled decision behind them.

**Model:** Armenia-Azerbaijan, 9 November 2026 — treaty unsigned, constitutional precondition, TRIPP ratification, CSTO/EU alignment, Margara ready; watch table runs to early December.

**Review rule:** the weekly watcher reviews it every run and rewrites only on a material change (see `content-update-policy.md` §3).

---

## 5. `updates/YYYY-MM-DD.md`

**Purpose:** the week's delta, in a form a reader can scan in thirty seconds.

**Must contain**
- Three to six bullets, each `- **Headline** — body` on one line.
- A headline that states the consequence, not the event type ("TRIPP becomes law", not "Parliament vote held").
- A body of one to three sentences: what happened, the number or name that makes it concrete, and why it matters.
- Source links at the end of the body in parentheses: `([OC Media](url), [Eurasianet](url))`.

**Must not contain**
- Background a reader already has from the current-situation or overview.
- More than one development per bullet; split it or drop the weaker one.
- Per-source summaries, "sources say", or a list of everything ingested.
- Anything about the ingest process (counts, ranges, PDFs, R2).
- Static-page changes. The watcher writes the update, not the entity page.

**Selection rule:** if a week produces more than six candidates, keep the ones that change a position, a deadline, a number that matters, or a relationship. Drop commentary, ceremonies and reactions that will be superseded.

**Model:** 2026-11-07 — seven bullets, each a distinct decision (ratification, trilateral groups, treaty timetable, detentions, court appointment, CSTO/EU split, border).

---

## 6. `articles/YYYY-qN.md`

**Purpose:** the quarter's argument, not its diary.

**Must contain**
- Frontmatter: `title`, `summary` (one or two sentences), `date` (quarter end).
- Body starting at `##`, not `#`.
- An opening "short version" of two paragraphs that states the quarter's central tension.
- Four to six thematic sections, each built on two or three developments that support one claim.
- Footnotes for every factual claim: `[^n]` in the text, `## References` then `[^n]: Publication, "Title", YYYY-MM-DD. URL` at the end. Reuse a number rather than duplicating a source.
- A closing "what to watch" list of three to five questions.
- The article's own synthesis, stated as argument. It should sit *after* the evidence, not replace it.

**Must not contain**
- A chronological recap of the quarter.
- Material from the following quarter — including quotes, data releases and events. Data about the quarter published later is acceptable only if the article is explicit about the period.
- Unattributed evaluative claims. "Analysts warned" is not attribution; name the analyst or outlet.
- One source carrying the thesis. Editorials must be labelled as opinion and used sparingly; facts should come from reporting.
- Only one side's sources in a bilateral topic. Include the other side's officials or outlets.

**Model:** 2026-q3 "The peace dividend arrives before the peace" — 26 footnotes, OC Media and Caucasus Watch for reporting, Caliber.Az for Baku's position, Modern Diplomacy cited once as an editorial, and a closing lock-in argument in the wiki's own voice.

---

## 7. `entities/<slug>.md`

**Purpose:** explain one actor's leverage over the topic, and the limits on it. Not a biography.

**Must contain**
- Frontmatter: `title`, `summary` (one sentence), `role` (people and states; for a group, a short descriptor). Optional `facts` and `weight`.
- An unheaded opening paragraph (2-3 sentences) directly under the H1: who they are *in relation to this topic*, and what they want.
- `## Key Actions` — four to six dated bullets, only decisions that moved the process.
- `## Current Position` — where they stand as of the last review, in 2-4 sentences. This is a structural position, not this week's news.
- `## Constraints` — three bullets on what limits them.

**Variants:** a non-state actor may use `## Role` and `## Controversy` instead of Key Actions/Constraints (Sokolov); a state under external pressure may use `## Key Interests` and `## Key Actions` (Iran). Keep the opening paragraph and the actor-first focus in every variant.

**Must not contain**
- Career history, party history, or personal detail with no bearing on the topic.
- A "Relevance to the topic" heading; the opening paragraph does that job.
- Duplicated `role`/`party` lines in the body when frontmatter already carries them.
- Weekly news. If a development changes the actor's position, the current-situation changes first; the entity changes only at review.

**Model:** Pashinyan (346 words), Aliyev (278), Iran (307).

---

## 8. `concepts/<slug>.md`

**Purpose:** explain a mechanism, dispute or idea the reader needs in order to follow the topic. It should answer "what is this and why does it decide things?" — not "what happened".

**Must contain**
- Frontmatter: `title`, `summary` (one sentence).
- `## Overview` — 2-4 sentences defining the thing and its stakes.
- Two to four sections that explain structure, not chronology: how it works, who wants what, where the disputes are.
- `## Current Status` or `## Open Issues` — the live state in 3-5 sentences.

**Variants:** a process page uses `## Why It Is Difficult` / `## The Process` (Border Delimitation); a legal-political dispute uses `## What X Demands` / `## Why It Is Hard` (The Constitutional Question); an infrastructure page uses `## Structure` / `## Strategic Significance` (TRIPP).

**Must not contain**
- A full history; only the events that explain the current structure.
- The same event narrated in three sections. One statement, then reference.
- Length beyond ~450 words without a specific reason (a genuinely multi-part mechanism).

**Model:** TRIPP (354 words), Border Delimitation (417), The Constitutional Question (388).

---

## 9. `timeline/<slug>-timeline.md` and `sources.md`

### Timeline

**Purpose:** the arc a new reader needs, at month resolution.

**Must contain** one `## YYYY` heading per year; month or season parents (`- **June:**`, `- **Fall:**`); every event as a two-space-indented sub-bullet; only defining events — leadership changes, agreements signed or blocked, wars and offensives, coercive economic moves, treaties, corridor openings.

**Must not contain** day labels, `###`, year ranges, prose paragraphs, commentary, or one event repeated in two months. Target 40-100 lines. Reviewed quarterly, not weekly.

### Sources

**Purpose:** the evidence base for everything else. Not a reading list.

**Must contain** the five-column table from the contract. Each summary states what the source *adds*: the specific fact, figure, or position, in one to three sentences. The publication is the clean outlet name; the date is ISO.

**Must not contain** near-duplicate coverage of the same event (pick the primary and note unique angles), aggregated listicles with no original reporting, or rows whose summary merely restates the headline. When two outlets carry the same wire copy, keep one.

---

## 10. Where a fact belongs

| If the new material is… | It belongs in… | Not in… |
|---|---|---|
| A decision, attack, appointment, deal, deadline | `updates/<date>.md` | entity, concept, overview |
| A shift in an actor's stance or leverage | current-situation now; entity at review | update only |
| A new mechanism or disputed concept | concept page | timeline |
| A defining historical event | timeline | update, overview |
| A pattern across weeks | article (quarterly) | updates |
| A number or quote that proves a claim | sources row, cited by the page that uses it | nowhere else |
| A framing of the topic | overview | current-situation, article |

**Duplication test:** before publishing, search the topic folder for the key noun and number. If the same fact appears in three files, decide which one is canonical and reduce the others to a clause or a link.

## 11. Sourcing and attribution

- **Hierarchy:** official statements and documents > specialist regional reporting (OC Media, Eurasianet, RFE/RL, JAMnews, Caliber.Az, Meydan TV) > general outlets > think tanks and editorials (analysis, labelled) > social media (only as a lead, never as the citation).
- **Balance:** in a bilateral topic, at least one source from each side's official position per major section. Armenia-Azerbaijan's Q3 article uses Caliber.Az and MassisPost alongside OC Media and Caucasus Watch.
- **Attribution verbs:** *reported* (fact), *said* (quote), *argued/assessed/estimated* (analysis), *according to* (data). Never "critics say" without naming them.
- **Verification pass:** open the cited page and confirm the sentence's specific detail — the person's title, the date, the period, the direction of the figure. A source that covers the topic is not evidence for the detail. A July report cannot confirm a September status.
- **Footnotes vs inline:** articles use numbered footnotes; updates use outlet links in parentheses; current-situation and static pages carry no footnotes, but every contested claim must be traceable to a `sources.md` row.

## 12. Pre-publish checklist

- [ ] Length within the target for the type.
- [ ] Every factual claim traceable; every interpretation attributed or visibly the wiki's argument.
- [ ] No material from after the page's date.
- [ ] No fact duplicated across three files without a canonical home.
- [ ] Both sides represented where the topic is bilateral.
- [ ] Frontmatter present and matching the H1.
- [ ] No stray leading pipes; tables are the only pipes.
- [ ] Index counts and `Total sources` updated when pages or rows change.
