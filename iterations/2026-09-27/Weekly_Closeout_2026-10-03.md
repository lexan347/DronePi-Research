# Weekly closeout — 2026-10-03

Week: Sunday 2026-09-27 through Saturday 2026-10-03 (America/New_York).
Status: DRAFT — week is not closed. Prepared on October 1; finalize after Saturday's work.

## October 1 preliminary summary (historical; see October 3 update)

- Intended candidate name confirmed as DronePi.
- Equipment and CAD version identified; missing capability checks recorded.
- Harmonic 8.15.0 and Citadel 3.15.1 each pass basic launch, rendering and execution checks.
- Hardware audit records unresolved purchase, power, mass, payload and interface questions.
- PX4 reference simulation setup instructions issued; downloads reported finished by user.

## October 1 handoffs (historical)

| From | To | Deliverable | Status |
|---|---|---|---|
| User | Software | PX4 post-reboot X500 terminal and GUI evidence | Pending |
| Engineering | Software | Supported mass, inertia, power and propulsion parameters | Pending |
| Software | Engineering | Integration constraints from reference simulator tests | Pending |
| Project lead + AI | All streams | Verified WBS mapping and NLT dates | Pending |

## Saturday finalization

Review every daily log. Record completed acceptance checks, evidence, decisions, unresolved blockers, schedule changes and next week's tasks. Do not mark planned work as complete. Correct any preliminary summary using dated entries. Numerical days gained require mapped schedule dates.

## Next week draft

Start Sunday October 4 with folder `iterations/2026-10-04/`. Continue reference-flight testing, CAD compatibility checks, hardware documentation closure and component costing in parallel.

## October 3 interim update — DRAFT

This update supersedes the preliminary setup status above. Day and week remain OPEN; no final closeout is asserted.

- October 2: 10 mm FreeCAD STEP/STL workflow checked, DronePi documentation and runtime reviewed, three-file repair passed 12 isolated regression checks and was committed locally. Full mission integration remains pending. See [October 2 log](Daily_Log_2026-10-02.md).
- Faculty recommendations implemented: visitor overview, simulation diagram/software inventory, reference vehicle image, available parameter evidence and daily research routine. Independent research remains for Alexander to supply.
- October 3: ROS Jazzy installed and talker/listener tested; DDS Agent and pinned px4_msgs built; PX4 bridge connected and ROS decoded telemetry. QGroundControl connected and preflight passed.
- X500 takeoff to an observed 5 metres, steady hover, landing and automatic disarming completed. Flight result is qualitative; duration and accuracy await log analysis. Grounded heading-flag concern resolved through source inspection and post-flight magnetic alignment evidence.
- Closed ULog copied and checksum verified by Alexander; [manifest](Flight_Manifest_2026-10-03.json) records exact revisions, size and checksum. Raw log remains local. See [October 3 log](Daily_Log_2026-10-03.md).
- The historical Citadel claim above is not the basis for current acceptance: the October 3 flight used native Gazebo Harmonic 8.15.0. Older launcher issues remain separate.

### Current handoffs and blockers

User-to-software reference simulator evidence is delivered. ROS telemetry reception is established. Camera plugin loading and DronePi mission integration remain open. Engineering-to-software mass, inertia, power and propulsion inputs remain pending. BOM closure, component costing, mapping accuracy targets, independent literature notes, separate backup and verified WBS mapping remain open.

### Schedule and next iteration

These preparatory checks were completed before the January 2027 work semester; no numerical schedule gain is claimed without mapped baseline dates. Final NLT remains May 5, 2027; cost ceiling remains $2,000. Begin the next Sunday–Saturday iteration October 4: software addresses camera capture and integration; engineering closes component/interface evidence; Alexander supplies research notes, decisions and measurements. Finalize this draft only after Saturday's remaining work is recorded.
