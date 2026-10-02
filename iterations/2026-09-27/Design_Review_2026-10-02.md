# DronePi design review — 2026-10-02

Status: preliminary static review; procurement hold pending a complete BOM and interface design.
Source: Xavier-Nieves/DronePi-Autonomous-Mapping, commit 57d720586f81b035187e65cb0358b1f58233b36e, supplied review ZIP.
Scope: README, 12 documentation files, dependency manifests, and 10 shell scripts. Application source was not included. No installation, flight, electrical, or hardware simulation was performed.

## Findings and required actions

| Priority | Finding | Evidence | Required action |
|---|---|---|---|
| Blocking | No build-ready aircraft BOM. Motors, ESCs, propellers, battery, charger, power distribution, RC system, wiring and fasteners lack a consolidated set of quantities and exact compatible parts. | docs/hardware_setup.md component tables | Build a purchased/printed/fabricated BOM with manufacturer specifications, quantities, landed costs and spares. Verify the complete build against the $2,000 ceiling. |
| Blocking | Power budget is not an interface design. It totals 19 W typical and 24.5 W peak, then treats the total as a 5 V load. | docs/hardware_setup.md section 3 | Separate voltage rails. Unitree's L1 manual specifies a 12 V, 1 A supply; identify the actual L1 adapter and its input requirements. Specify converters, battery voltage range, protection, connectors and wiring. Model losses, startup and worst-case loads before bench validation. |
| Blocking | Existing photo mosaic is not orthorectified. It uses panoramic stitching plus GPS positioning and can fall back to a collage. Full Orthorectifier is explicitly unimplemented. | docs/post_processing.md, Stage 3; README Known Open Items | Plan and validate a true orthomosaic pipeline. Agree numerical map/3D accuracy criteria and ground truth checks; maximum sensor resolution alone is not an accuracy criterion. |
| Blocking | Root setup.sh computes PROJECT_DIR as its parent directory, whereas helper scripts live under setup_scripts. Its documented invocation points to setup_scripts/setup.sh, absent from the packet. | setup.sh path definitions and run_sub calls; archive layout | Correct paths in an isolated working copy and validate all service entry points against the full source before installation. |
| High | Setup targets a Pi ARM64 system and hardcodes the dronepi account/home. It downloads an aarch64 installer and changes packages, system services, device rules and networking. | setup.sh | Create a separate x86_64 workstation environment recipe. Do not run the aircraft setup script on the current Intel workstation. |
| High | ROS build can report success after a failed colcon build: an inner bash command pipes output to tail without its own pipefail. | setup.sh ROS workspace build | Preserve the builder exit status and full logs. A syntax pass is not an installation pass. |
| High | Component descriptions conflict: README identifies Hailo-8L as 26 TOPS, while hardware documentation says Hailo-8. | README and docs/hardware_setup.md | Choose exact part only if an AI workload is required. Raspberry Pi specifies Hailo-8L at 13 TOPS and Hailo-8 at 26 TOPS. Integration is listed as pending. |
| High | Flight-controller wiring mixes TELEM2 UART and direct USB descriptions; GPS and RC descriptions are insufficient to select compatible hardware. | docs/hardware_setup.md | Create separate USB/UART pinouts and identify logic voltage, grounding, adapters, GPS module and receiver protocol. |
| High | Camera remount, real-data texture validation, OFFBOARD consistency and full mission tests remain open upstream. | README Known Open Items | Treat upstream statements as reported status. Reproduce required checks on our pinned configuration before crediting them as passed. |
| High | Dependency versions and external source revisions are not fully locked. | pip_requirements.txt, conda_requirements.yaml, setup.sh | Produce platform-specific locks and pin external SDK/SLAM commits. Verify compatibility using actual runtime imports and build configuration. |

## SWaP and simulation readiness

SWaP means Size, Weight and Power; SWaP-C adds Cost. Aircraft geometry, complete component masses, battery/propulsion data and payload mounting are insufficient for a defensible flight model. Connectivity and voltage checks can begin with an interface table, but simulation cannot prove undocumented connectors, missing parts or hardware reliability.

Required model inputs: airframe dimensions; component masses and centers; motor/propeller thrust-current data; ESC limits; battery capacity, voltage and discharge limits; converter efficiency; sensor field of view/range; mounting transforms; cable/connector specifications; target flight envelope.

## Verification completed

All 10 shell scripts passed bash -n syntax parsing. They were not executed. Documentation explicitly confirms that the full orthorectification path is planned. Static inspection confirms the setup path mismatch and ARM64 installer selection. No runtime compatibility, complete BOM, cost fit, flight performance or electrical design has been certified.

## Parallel work and handoffs

| Stream | Next work | Handoff |
|---|---|---|
| Hardware and CAD | Extract a complete BOM from DronePi and LANDRs; identify missing parts; build mass, cost and voltage-rail tables. | Exact parts and interfaces to simulation/software; mounts to CAD. |
| Software and simulation | Review application source; correct setup assumptions in a separate working copy; define reproducible desktop environment. | Required interfaces, logging and workloads to hardware; measured resource loads after runtime tests. |
| Mapping and validation | Define orthomosaic and 3D acceptance measures for Lead Mills; plan ground truth and evaluate the missing orthorectification work. | Camera/LiDAR requirements and validation datasets to both streams. |

Purchasing waits for compatible parts, a closed cost estimate and a reviewed power/interface design. Schedule dates remain no-later-than markers; ready tasks start early.

## Daily activity supplement

The user located LANDRs-Science-Drone-main.zip and Hardware-master.zip. The archive inventories show mechanical CAD/assembly material in LANDRs and flight-controller board design material in Hardware-master; neither inventory alone establishes a complete drone kit. DronePi was cloned with a clean reported working tree, pinned to the commit above, and a documentation/setup review packet was created. The current review establishes the gaps above; it does not establish that any candidate is ready to order.

## Manufacturer references

- Unitree L1 user manual: https://oss-global-cdn.unitree.com/static/f5ca3e9038d44ca29f711f90005a2185.pdf
- Raspberry Pi AI HAT documentation: https://www.raspberrypi.com/documentation/accessories/ai-hat-plus.html
