[IMPORTANT: You are running as a scheduled cron job. DELIVERY: Your final response will be automatically delivered to the user — do NOT use send_message or try to deliver the output yourself. Just produce your report/output as your final response and the system handles the rest. SILENT: If there is genuinely nothing new to report, respond with exactly "[SILENT]" (nothing else) to suppress delivery. Never combine [SILENT] with content — either report your findings normally, or say [SILENT] and nothing more.]

You are maintaining a research wiki on {topic_name}, cloned at /root/wiki on GitHub (repo: clawrl-hermes/whats-going-on-with). This topic lives in /root/wiki/{slug}/. Use the git credential helper for auth (no gh CLI).

TASK: Search for new sources on {topic_name} and add any substantive new findings to the wiki. Check curated priority sources first if available, then run broader Tavily searches.

Step 0a: Read /root/wiki/{slug}/domain-notes.md for topic-specific context — search queries, key data points, dedup pitfalls, and entity tracking guidance.

Step 0b: Check if priority-sources.md exists at /root/wiki/{slug}/priority-sources.md. If it does, read it and follow this order:
  - First, for each Regional Specialist and Official Source listed, use tavily_extract on their main page URL to find articles published in the last 7 days
  - Check Think Tanks for analytical context on recent developments
  - Check Advocacy & Diaspora sources for Congressional/diaspora tracking
  - Only after exhausting priority sources, proceed to Step 2
  If priority-sources.md does NOT exist, skip directly to Step 1.

Step 1: Read /root/wiki/{slug}/sources.md to understand what sources already exist (so you do not add duplicates).

Step 2: Run the following Tavily searches using the tavily_search tool:
{search_queries}

For each search, use time_range="month" and max_results=5. Add a 3-5 second delay between consecutive searches to avoid HTTP 429 rate limit errors.

Step 3: For each promising new source found, use tavily_extract to get full content.

Step 4: For each substantive new source:
  a. Summarize key findings in 2-3 sentences
  b. Append a row to /root/wiki/{slug}/sources.md in the five-column shape:
     | N | Publication | [Title](url) | YYYY-MM-DD or YYYY-MM | Summary |
     Publication is the clean outlet name, not an "Outlet: " prefix inside the title. Use exactly one leading pipe.
  c. If the source contains date-relevant events, add them to the timeline as two-space-indented sub-bullets under the month/season parent
  d. Update relevant entity/concept pages; any new page needs `title` and `summary` frontmatter
  e. Update /root/wiki/{slug}/index.md (increment source count, update date)

Step 4a: Write /root/wiki/{slug}/updates/<YYYY-MM-DD>.md for today's run — 3 to 6 bullets on what changed, each in the form `- **Headline** — body` on one line. No frontmatter and no title. This is the site's weekly update and is not optional; if nothing substantive changed, still write a short file or report that clearly.

Step 5: Append an entry to /root/wiki/{slug}/log.md in this shape:
  ## YYYY-MM-DD - Weekly Source Update
  - New sources ingested:
    - N from priority sources
    - N from Tavily
  - Updated sources.md (old → new), index.md source count (old → new)
  - Updated timeline with N new entries (month range)
  - Updated <entity> entity: one-clause description
  - Updated <concept> concept: one-clause description
  Counts and page names only — never per-source titles, URLs, or summaries.

Step 6: Commit and push changes:
  cd /root/wiki
  git pull --rebase
  git add {slug}/
  git commit -m "Weekly source update ({slug}): [brief summary of what was added]"
  git push

Step 7: Review whether domain-notes.md needs updating. Update only structural context — new key data points, search queries, dedup pitfalls, high-signal source types, or entities. Do NOT add a "Key Recent Developments" section; recent events belong in the timeline and the update file. Keep one Trackable Indicators table.

Step 8: Deliver your final response using this notification format (the system sends it automatically):

# {Topic Name} — Weekly Source Update
**Date:** {date} | **Sources:** {old_count} → {new_count} ({added_count} new)

For each new source, include: | {N} | {Publication} | [{Title}]({url}) | {YYYY-MM-DD} | {1-2 sentence key finding} |

Then include a **Key Themes This Week** section (max 5 bullet points) and a **Files Updated** section.

IMPORTANT: Only add sources with real, substantive new information. Quality over quantity. If no new sources were found, report that clearly instead of the table.
