# DronePi application code review — 2026-10-02

Status: first-pass review complete; runtime integration and aircraft testing pending. DronePi remains a provisional reference design.

Archive: DronePi-code-review-57d7205.zip. ZIP commit comment matches 57d720586f81b035187e65cb0358b1f58233b36e. Contents cover unitree_drone_mapper, rpi_server and ground_station_app, with 228 ZIP entries and 233,196,045 uncompressed bytes. Existing example meshes and metadata are included; they are not evidence of our mission performance. RPI5 ROS workspace and external SDK sources are outside this packet.

## Verified defects and integration gaps

| ID | Priority | Evidence at pinned revision | Effect and required correction |
|---|---|---|---|
| C-01 | Blocking | main.py: MainNode.fly_to(), lines 260–283. Timeout returns true whenever override/abort flags are false. handle_autonomous() interprets true as waypoint reached. | An unreached waypoint can be logged as reached and trigger a camera action. Return an explicit timeout result; stop or recover under a defined mission policy. Add a regression check before SITL. |
| C-02 | Blocking | main.py command definitions reference sibling slam_bridge.py and postflight.py; neither exists under unitree_drone_mapper in the archive. Existing implementations are flight/_slam_bridge.py and utils/run_postflight.py. | Bridge/postflight commands target absent files. Correct entry points and validate subprocess readiness and exit status. Do not assume renaming alone resolves session and command-line contracts. |
| C-03 | Blocking | dronepi-main.service invokes main.py without arguments; main.py requires --waypoints. | This shipped service command exits at argument parsing rather than starting a mission. Resolve how missions are loaded and who owns the mission process before enabling services. |
| C-04 | High | main.py: start_pointlio() and start_slam_bridge() sleep then return true after Popen, with output discarded and no process/readiness check. | Failed child commands can appear started. Require live process plus fresh expected ROS data; retain logs and propagate failures. |
| C-05 | High | WaypointValidator.check() skips the entire radius check if GPS is unreliable; it does not reject non-finite coordinates or constrain altitude. | Pure logic probes accepted a 1,000 m horizontal waypoint with GPS unavailable, NaN with reliable GPS, and 10,000 m altitude. Enforce finite values and local horizontal/vertical limits independently of GPS. Add site boundary checks; a radius check alone cannot identify a mission intended for another site. |
| C-06 | High | MosaicBuilder.build() returns a collage together with precomputed geo bounds when GPS compositing fails. postprocess_ortho.py labels fallback only using geo is None. | A collage can be marked collage_fallback=false and receive a world file. Return explicit output type and placement status; refuse measurement/georeferencing claims for collage output. |
| C-07 | High | camera_capture.py sets main image size to 2028×1520. camera_calibration.yaml specifies 4056×3040 intrinsics. CameraModel loads those values directly; TextureProjector applies them to actual image dimensions. | Capture and calibration contracts differ. Projection can reject or misplace colours. Choose capture mode, calibrate it, and validate any crop/binning/intrinsic scaling. Current capture setting does not satisfy the user's full-resolution goal automatically. |
| C-08 | High | main.py: trigger_camera() publishes a command topic through subprocess.run(), does not check returncode and logs Camera triggered after any normal return. No CameraCapture instance is wired into main.py. | A failed command can be logged as successful. Trace the actual capture recipient and saved-image acknowledgement; require a frame and sidecar tied to the waypoint/session. End-to-end capture is unverified. |
| C-09 | High | main.py landing finalizer waits at most 45 s, then stops SLAM/Point-LIO and tears down regardless of remaining armed state. | Cleanup can occur without confirmed landing/disarm. Define and simulate prolonged landing, rejected LAND and lost telemetry outcomes. Retain required flight-estimation services until a verified safe state or explicit pilot handoff. |
| C-10 | Medium | run_postflight.py deliberately leaves orthomosaic failure out of its exit code. | A mesh-only success cannot count as completion of our two-output requirement. Record mesh and photo-map outcomes separately; overall project acceptance requires both. |

## Mapping clarification to the earlier documentation review

Actual MosaicBuilder code defaults to GPS/SLAM-anchored rectangular image placement. Panoramic cv2 stitching is opt-in. The documentation description of stitching as the default is stale. The default compositor resizes and places images without terrain orthorectification or full camera-attitude projection; it is not a validated orthomosaic.

postprocess_ortho.py accepts --ortho-tif to tile an externally generated georeferenced GeoTIFF. This provides a possible downstream integration route; it does not generate that orthophoto. The full Orthorectifier remains planned and there is no --full CLI option at this revision.

The earlier [Design_Review_2026-10-02.md](Design_Review_2026-10-02.md) is a documentation-only snapshot. This source review supersedes its description of the default mosaic path.

## Verification performed

- Parsed all 121 Python files with ast.parse: no syntax errors.
- Checked the bridge/postflight sibling paths against the supplied source tree: missing.
- Executed extracted methods only with fake clocks, fake GPS, fake ROS calls and fake image/compositor objects. No ROS node, network service, aircraft command, camera or upstream installer was started.
- Timeout probe: no movement, clock beyond timeout, override flags false -> fly_to returned true.
- Collage probe: GPS bounds exist, compositor returns none -> collage returned with geo retained; downstream fallback expression evaluates false.
- Waypoint probes: GPS unavailable + 1,000 m waypoint -> passed/skipped; reliable GPS + NaN -> passed; reliable GPS + 10,000 m altitude -> passed.

These checks reproduce control-flow defects. They are not SITL, full application tests, dependency installation checks or hardware simulation. ROS/MAVROS/Point-LIO versions, frames, timing, covariance and failure behaviour still require integration verification.

## Repair and validation handoffs

| Stream | Immediate work | Completion evidence |
|---|---|---|
| Software | Prepare isolated working branch, correct mission entry points, subprocess readiness, waypoint timeout/limits and capture acknowledgements. | Regression checks plus controlled SITL covering timeout, invalid input, startup failure, OFFBOARD loss and landing failure. |
| Mapping | Correct fallback metadata, choose/calibrate capture mode, review external orthophoto integration and enforce separate output outcomes. | Known-ground-truth image set, matching calibration, verified georeferencing and separate mesh/map acceptance results. |
| Hardware/CAD | Continue complete BOM, voltage rails, mass, mount and budget closure. | Exact compatible parts and interface data handed to simulation; no purchase decision based only on this source review. |

Dates remain no-later-than markers. Do not credit syntax checks or upstream example outputs as finished integration. Next software milestone is a reproducible workstation environment and a corrected mission skeleton in SITL; live-aircraft tests follow only after these checks and hardware review.
