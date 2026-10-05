# Resume plan — October 5 pause

Day remains OPEN. No unattended local test is running on behalf of the assistant. The assistant has GitHub documentation access, not remote terminal access to Alexander's workstation.

## Preserve before further experiments

Confirm whether the last config-copy/checksum commands ran. Retain camera_check_092958 and its samples. The existing bag closed cleanly; two transport losses are recorded. Do not rerecord just to recover these files.

## If applications remain open

Do not launch duplicate simulators/agents/bridges. Check that Gazebo is playing, x500_depth_0 and depth_target_3m exist, and ROS image topics still deliver. Remain grounded for depth tests.

## If applications were closed or the workstation rebooted

Open separate terminals for the following processes:

```bash
# Terminal 1: PX4 telemetry agent
source /opt/ros/jazzy/setup.bash
source ~/drone-project/ros2_ws/install/local_setup.bash
MicroXRCEAgent udp4 -p 8888
```

```bash
# Terminal 2: native simulation; use a fresh terminal without ROS sourcing
cd ~/drone-project/PX4-Autopilot
make px4_sitl gz_x500_depth
```

Open the existing QGroundControl launcher. Then:

```bash
# Terminal 3: image bridge
source /opt/ros/jazzy/setup.bash
ros2 run ros_gz_bridge parameter_bridge   '/world/default/model/x500_depth_0/link/camera_link/sensor/IMX214/image@sensor_msgs/msg/Image[gz.msgs.Image'   '/depth_camera@sensor_msgs/msg/Image[gz.msgs.Image'   --ros-args   -r /world/default/model/x500_depth_0/link/camera_link/sensor/IMX214/image:=/camera/image_raw
```

The inserted target is a runtime entity and will need re-creation after a new world starts. First inspect the new vehicle pose; the saved placement assumes the October 5 grounded pose. Native inspection from a ROS-sourced shell:

```bash
env -u GZ_CONFIG_PATH /usr/bin/gz model -m x500_depth_0 --pose
```

Next task: automate 1/3/5 m tests using multiple distinct sensor timestamps. Predeclare tolerances and sample count; collect compact JSON/CSV instead of another multi-gigabyte bag. Keep two-loss transport investigation separate from geometric accuracy.

## Pause/shutdown

Grounded/disarmed state was shown before pause; subsequent shutdown is not confirmed. To stop when grounded, Ctrl+C in the image bridge, then PX4 simulation terminal, then agent terminal; close remaining GUI windows normally. Confirm exits rather than assuming the camera window closes every background process.

## End-of-session updates

Append outcomes to the same daily log; update weekly status, overview and simulation configuration when changed. Capture exact commands/versions, evidence, warnings, unconfirmed steps, next tasks and Alexander's own research notes. Only mark the day CLOSED when the user requests closeout; Saturday summarizes the Sunday–Saturday iteration.
