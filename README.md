# DronePi Research

Senior research project for a modular survey drone. Preferred candidate: [DronePi Autonomous Mapping](https://github.com/Xavier-Nieves/DronePi-Autonomous-Mapping). Candidate selection is provisional pending documentation, hardware, software, and cost checks.

Hands-on semester begins January 2027. Final delivery is no later than May 5, 2027. Schedule dates are No Later Than markers; complete tasks early when dependencies and acceptance evidence permit.

## Start here — repository overview

Updated October 3, 2026. Goal: evaluate and build a modular mapping drone producing aerial photo maps and 3D models within a $2,000 purchase ceiling. Lead Mills is the first proposed field site.

**Current stage:** PX4/Gazebo X500 reference simulation and DronePi source evaluation. The proposed aircraft has not yet been modeled or validated. Twelve isolated repair checks passed on the Linux workstation. On October 3, ROS telemetry reception and a QGroundControl-operated X500 takeoff, observed 5-metre hover and landing were demonstrated. Full DronePi integration remains pending.

| Section | What you will find |
|---|---|
| [Simulation environment](Simulation_Environment.md) | Faculty questions 1–3, architecture diagram, software inventory, model image, configuration evidence and gaps |
| [Design review](iterations/2026-09-27/Design_Review_2026-10-02.md) | BOM, power, interfaces and documentation gaps |
| [Code review](iterations/2026-09-27/Code_Review_2026-10-02.md) | Reproduced software defects and integration limits |
| [Verified repair checkpoint](iterations/2026-09-27/Repair_Checkpoint_2026-10-02.md) | Local commit, test results and archived patch |
| [Daily log](iterations/2026-09-27/Daily_Log_2026-10-03.md) | Chronological activity and evidence |
| [Daily plan](iterations/2026-09-27/Plan_2026-10-02.md) | Parallel work and handoffs |
| [Weekly closeout](iterations/2026-09-27/Weekly_Closeout_2026-10-03.md) | Saturday summary, currently draft |
| [Decisions](DECISIONS.md) | Rationale and project choices |
| [End-of-day routine](End_of_Day_Routine.md) | Reproducibility, documentation and research checks |
| [Independent research notes](Research_Notes_Template.md) | Alexander's reasoning, sources personally read and comparison with AI assistance |

**Faculty question 4:** This README is the visitor overview and navigation index. Dated iterations retain the evidence and history behind each conclusion.

## Weekly iterations

Weeks run Sunday through Saturday in America/New_York. Folder names use the Sunday start date: `iterations/YYYY-MM-DD/`. Daily logs use `Daily_Log_YYYY-MM-DD.md`; Saturday closeouts use `Weekly_Closeout_YYYY-MM-DD.md` with Saturday's date. Update the same daily file after each work session; Git history preserves earlier entries. Never create fictional activity for days without evidence.

Current iteration: [September 27–October 3, 2026](iterations/2026-09-27/Weekly_Closeout_2026-10-03.md).

## Three parallel streams

| Stream | Responsibilities | Handoff |
|---|---|---|
| User / project lead | Decisions, computer setup, measurements, faculty coordination, fabrication and field work | Evidence and decisions to both technical streams |
| AI engineering | BOM completeness, interfaces, power, mass, payload and CAD analysis | Documented assumptions and model parameters to software |
| AI software | Repository review, dependency checks, simulator setup and integration | Test results and missing interface requirements to engineering |

These are responsibility streams. They do not imply unattended agents or scheduled work are running.

## Logging rules

Record activity, owner, status, evidence, decisions, blockers, next action, and WBS reference. Use actual workbook WBS IDs only when verified; otherwise mark `Unmapped`. Distinguish user-reported completion, independently reviewed evidence, assumptions, and planned work. A reference simulator test does not validate the proposed aircraft.

Saturday closeout summarizes verified work, incomplete handoffs, blockers, schedule gains supported by dates, and next week's tasks. Keep corrections visible rather than rewriting history silently.

## Repository contents

Original project documentation belongs here. Keep upstream PX4/DronePi source in separate clones; record source URLs and versions instead of copying whole projects into weekly folders. Large ZIPs, build output, credentials, personal correspondence, and site boundary files are excluded from this initial public documentation. No license is assigned to original work yet; upstream licenses still apply to their code.

See [decisions](DECISIONS.md) and [log templates](templates/Log_Templates.md).
