# Content update policy

**Status: draft for review — 2026-11-10.** This file defines *when each file is reviewed and who may change it*. What each file should say is in `content-substance.md`; format and the publish allowlist are in `content-contract.md`.

The principle: **ingestion and interpretation run on different clocks.** Weekly work records what changed. Periodic work decides what it means for the standing pages.

---

## 1. Two jobs, one boundary

| Job | Owns | Cadence | May not touch |
|---|---|---|---|
| **Weekly source monitor** (existing cron) | `sources.md`, `updates/<date>.md`, `log.md`, `current-situation.md` review, index counts | Weekly | `overview.md`, `timeline/`, `entities/`, `concepts/`, `domain-notes.md`, `articles/` |
| **Static content review** (one job per topic) | `overview.md`, `timeline/`, `entities/`, `concepts/`, `domain-notes.md`, corrections to `index.md` counts | Monthly or event-driven | `sources.md`, `updates/`, new fact-finding |

The weekly job **does not edit static content**, even when it spots an error. It records the mismatch in its run report (not in the published update) and the static review acts on it. This keeps the weekly diff small and reviewable, and stops the same fact being re-litigated every week.

The static review **does not ingest**. It works only from what the weekly job already added to `sources.md` and `updates/`. If it needs a fact that is not there, it flags the gap for the next weekly run; it does not search for new sources itself.

---

## 2. Cadence by file

| File | Owner | Normal cadence | Change allowed |
|---|---|---|---|
| `sources.md` | Weekly | Every run | Append rows only; never rewrite history |
| `updates/<date>.md` | Weekly | Every run | New file; corrections only with a note |
| `log.md` | Weekly | Every run | Append counts-only entry |
| `current-situation.md` | Weekly (review) | Every run, rewrite only on material change | Full rewrite when triggered; otherwise untouched |
| `index.md` | Weekly (counts) / Static (catalog) | Counts each week; catalog at review | Counts only, then full catalog at review |
| `domain-notes.md` | Static | Monthly or event | Search queries, data points, dedup pitfalls, source types, indicators — no developments |
| `overview.md` | Static | Monthly or event | Rewrite only when the topic's central question changes |
| `timeline/` | Static | Monthly or event | Add defining events; condense; never append news |
| `entities/` | Static | Monthly or event | Update position/limits; no weekly news |
| `concepts/` | Static | Monthly or event | Update status; add a section only for a new mechanism |
| `articles/` | Static | Quarterly | New file per quarter; no retroactive edits beyond corrections |

A topic with four weekly updates a month therefore produces four small commits and at most one static-review commit.

---

## 3. The current-situation review rule

Every weekly run ends by re-reading `current-situation.md` against the update it just wrote. Rewrite **only** if at least one of these is true:

1. **A position changed** — an actor accepted, rejected or redefined a demand.
2. **A dated decision was taken or missed** — a vote, signing, deadline, court ruling, election.
3. **A deadline moved** — new date, slipped date, or a scheduled event cancelled.
4. **An anchoring number shifted materially** — a ratification margin, a trade share, a deployment, a gas volume.
5. **An actor entered or left** the story in a way that changes the open question.

If none applies, leave the page untouched, including `last_updated`. Do not refresh wording for its own sake.

When rewriting:
- Replace the whole page: the 3-5 status sentences, the open question, and the watch table. Never append to the old table.
- `last_updated` is the revision date, not the newest source's date.
- The watch table covers the next four weeks from the revision date; remove rows whose date has passed.
- Cap: one rewrite per weekly run. If two material changes land, the more consequential one defines the page; the other is captured in the update.

---

## 4. When static content is reviewed

Run a static review when **any** of these fires:

| Trigger | Timing | Scope |
|---|---|---|
| **Monthly cycle** | Monthly (default) | All static pages for the topic |
| **Structural event** | Within one week | The pages the event touches |
| **Quarter boundary** | Before the quarterly article | Timeline, entities, concepts, overview |
| **Reported error or contradiction** | Next review | The affected page, plus a search for the same error |
| **Actor or concept obsolete** | Next review | Merge, retire or fold into another page |

**Structural events** include: a peace treaty signed or abandoned; a government or leader change; war, offensive or ceasefire; a corridor or border opening; a sanctions or trade regime change; a constitutional amendment adopted or defeated; a major realignment (CSTO exit, EU candidacy).

Everything else waits for the monthly cycle. A minister's speech or a single poll is not a structural event.

---

## 5. Static review procedure

1. **Gather.** The last four to six `updates/`, the current `current-situation.md`, the timeline, and `git log --stat` since the last `Static Content Review` entry. Note what changed in `sources.md` but is not yet reflected anywhere.
2. **Triage each page.** Mark it: *no change* / *wording* / *structural*. Only structural changes should alter the page's argument or section order.
3. **Cap the blast radius.** At most five pages per monthly cycle unless a structural event justifies more. Prefer the pages a reader would consult first.
4. **Apply the substance rules.** Use `content-substance.md` per file type. Keep the actor-first test: does this change how the actor affects the topic?
5. **Timeline.** Add only defining events, under the correct month parent. If an event is already in an update but is not defining, it does not enter the timeline.
6. **Entities.** Update `Current Position` only if the actor's stance or leverage changed. Do not turn `Key Actions` into a news log — a new bullet must be an action that moved the process.
7. **Concepts.** Update the status section. Add a new section only when a genuinely new mechanism appears (a new corridor, a new legal instrument).
8. **Domain notes.** Review the search queries, key data points, dedup pitfalls, high-signal source types and the single `Trackable Indicators` table. Fold in what the last month of runs learned. No chronology, no `## Key Recent Developments`. Authoring rules are in `SKILL.md` → Create or Update Domain Notes.
9. **Overview.** Change only if the central question changed. `tagline`, `region` and `started` require the user's approval.
10. **Verify and balance.** Run the citation check from `content-substance.md` §11. For bilateral topics, confirm both sides are represented.
11. **Close the loop.** Update `index.md` counts and catalog. Commit as `static review: <topic> <date>`. Add to `log.md`:

    ```
    ## YYYY-MM-DD - Static Content Review
    - Reviewed: pages changed
    - Basis: updates <range>
    - Reason: what triggered the review
    ```

    If nothing needed changing, make no commit and say so in the job output — a no-op is a valid result.

---

## 6. What not to change at review

- **Overview framing** — tagline, region, started, and the central question are user decisions, not maintenance.
- **A fact resting on a single unconfirmed source** — wait for the next update or a second source. Note it; do not "fix" it.
- **A published article's argument** — corrections to facts are allowed and noted in the commit; retrofitting later analysis is not.
- **`sources.md` rows** — the reviewer does not add or delete sources. Gaps go back to the weekly job.
- **Entity pages for actors with no new actions** — leave them alone even if the cycle fires.

---

## 7. Rollout plan

1. **Review these guidelines.** No topic content changes yet.
2. **Update the seven weekly cron prompts** to: stop editing static pages, add the current-situation review step, and record static mismatches in the run report rather than the update.
3. **Create one static-review job per topic**, each running monthly, with its own commit and the log entry above. Separate jobs keep failures isolated and let topics run on different dates.
4. **Pilot on one topic** — Armenia-Azerbaijan is already the reference — for one cycle. Adjust the caps and triggers before applying to the rest.
5. **Then standardise the remaining topics**, one at a time, with the user reviewing each.

---

## 8. Quick reference

| Question | Answer |
|---|---|
| Can the weekly job fix an entity page? | No. Flag it; static review decides. |
| Can the weekly job update domain-notes.md? | No. It reads it for context; the static review maintains it. |
| Can the weekly job rewrite current-situation every week? | Only on a material change; otherwise leave it. |
| Can a static review add a new source? | No. It works from `sources.md`. |
| How often is the timeline touched? | Monthly, or after a structural event. |
| What if a static page contradicts a new update? | The update is authoritative for the new fact; the static page is corrected at review, not in the weekly commit. |
| How do we know when the last static review was? | The `Static Content Review` entry in `log.md`, and the commit history. |
| What if nothing changed? | No commit; report a no-op. |
