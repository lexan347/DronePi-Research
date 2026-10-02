# End-of-day and Saturday closeout routine

Effective October 2, 2026. Weeks are Sunday–Saturday; dates and session times use America/New_York. Apply this checklist when Alexander closes a work session. It is a working procedure, not an unattended scheduled job.

## Daily closeout

1. Update the existing `iterations/YYYY-MM-DD/Daily_Log_YYYY-MM-DD.md` for the Sunday-start iteration. Record activity, owner, result, evidence links, decisions, blockers and next handoff. Distinguish user report, independently checked evidence, inference and planned work.
2. For each simulation, record the run ID, purpose, reference or candidate vehicle, exact launch command, OS/software versions, Git/submodule commits, local changes, SDF/URDF and dependencies, world, physics/sensor settings, payload assumptions and PX4 parameters. Link configuration snapshots, logs and a labeled screenshot. Mark unavailable historical values as unknown.
3. Check the simulation diagram against the actual connections. Mark proposed ROS/SLAM/mapping components as planned until demonstrated. Keep the vehicle image and model description current.
4. Record expected versus observed results and acceptance criteria. Separate GUI startup, isolated code tests, SITL, hardware tests and field mapping. Record failure and shutdown state; do not turn partial success into a flight-readiness claim.
5. Ask Alexander for his own short research note: What am I trying to learn? Why this design? What assumptions might be wrong? What did I conclude before seeing the AI analysis? Preserve his words and authorship; AI edits must be labeled.
6. Ask what original literature Alexander personally read. Record query/database, full citation or DOI/URL, pages/sections, method, findings, limitations and relevance. Compare his reading with AI suggestions: agreement, disagreement, missing evidence and resulting decision. Use [Research_Notes_Template.md](Research_Notes_Template.md); mark not yet supplied rather than inventing a review.
7. Refresh the README navigation and affected overview pages; check relative links and image captions. Archive code patches and test evidence under the relevant iteration. Record the commit and whether local-only or published; omit credentials, personal correspondence and restricted data.
8. List tomorrow's must-completes across project lead, engineering and software streams, with dependencies and handoffs. Reference verified WBS IDs or mark Unmapped. Dates remain no-later-than markers; claim schedule gains only against a documented baseline.
9. Mark the daily log CLOSED only when requested to close. Carry unresolved tasks forward explicitly; a missing artifact is a blocker, not a completed task.

## Saturday closeout

Summarize verified results from Sunday through Saturday, open defects, incomplete evidence, independent literature findings, decisions and changes to assumptions. Review software/configuration reproducibility and repository navigation. Compare progress with the WBS/Gantt baseline, state justified gains or slips, and allocate the next week's parallel tasks. Preserve the week as an iteration; do not overwrite historical results with later conclusions.

## Paste into each daily log

```markdown
### End-of-day review
- Run/configuration evidence and diagram updated:
- Vehicle image/model provenance:
- Expected versus observed outcomes:
- Alexander's independent reasoning (verbatim or labeled edits):
- Sources personally read and critical notes:
- Comparison with AI findings:
- Decisions / assumptions changed:
- Git checkpoint and publication status:
- WBS reference / NLT marker:
- Blockers and next parallel handoffs:
- Tomorrow's must-completes:
- Day status: OPEN / CLOSED
```
