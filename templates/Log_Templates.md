# Daily and weekly log templates

Use America/New_York dates. Weeks start Sunday and end Saturday.

## Daily file: iterations/YYYY-MM-DD/Daily_Log_YYYY-MM-DD.md

# Daily activity log — DATE
Week: SUNDAY through SATURDAY. Status: Open / session complete.

### Activities
| Stream / owner | Activity | Status | Evidence | Handoff / next action | WBS / NLT |
|---|---|---|---|---|---|

### Decisions
Record the decision, who made it, basis and downstream impact.

### Tests and results
Record exact versions, inputs, expected outcome, observed outcome and evidence. Label user reports separately from reviewed output.

### Blockers and next actions
Record owner and action needed. On a day without project work, record no project work reported rather than inventing progress.

### Session updates
Append dated local-time notes when known; do not invent session times. Preserve corrections and Git history.

## Saturday file: Weekly_Closeout_YYYY-MM-DD.md

# Weekly closeout — SATURDAY
Week: SUNDAY through SATURDAY. Status: Draft / Closed.

- Verified completions and evidence by stream.
- WBS/NLT mapping and schedule gains or slips supported by dates.
- Decisions and corrected assumptions.
- Accepted and pending handoffs.
- Blockers, owners and resolution actions.
- Next Sunday's iteration and parallel tasks.
- List of daily logs reviewed; explicitly note missing evidence.

After closeout, retain the week's files. Put later corrections in a dated note or follow-up commit; never erase the original closeout silently.
