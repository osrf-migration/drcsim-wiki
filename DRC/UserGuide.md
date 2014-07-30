# DRCSim User Guide

DRCSim is a collection of models, environments, plugins, and tools that customize the Gazebo simulator for use in the DARPA Robotics Challenge (DRC).  Gazebo contains general simulation capabilities and DRCSim includes the robots, objects, and code that are specific to the DRC.  DRCSim is versioned and released independently of Gazebo.  Releases are recorded in the [[DRC/Change_log|change log]] and future plans are recorded in the [[DRC/Roadmap|roadmap]].

## Installation

[[DRC/Install|Full installation instructions]]

Quickstart for binary installation on Ubuntu 12.04 (precise):

    sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu precise main" > /etc/apt/sources.list.d/ros-latest.list'
    sudo sh -c 'echo "deb http://packages.osrfoundation.org/drc/ubuntu precise main" > /etc/apt/sources.list.d/drc-latest.list'
    wget http://packages.ros.org/ros.key -O - | sudo apt-key add -
    wget http://packages.osrfoundation.org/drc.key -O - | sudo apt-key add -
    sudo apt-get update
    sudo apt-get install drcsim

Note that the first four steps are only needed the first time you install; after that, the `apt-get` calls are sufficient.

## Setup

Before using DRCSim, you should configure your shell with the provided shell setup file

    source /usr/share/drcsim/setup.sh

'''You must load this setup file in every shell from which you're using DRCSim.'''  You may find it convenient to add the `source` line to your default shell configuration (e.g., `~/.bashrc`).
No noise added.
## Starting and stopping DRCSim

It's easiest to launch DRCSim using [http://ros.org/wiki/roslaunch roslaunch].  DRCSim includes several [http://ros.org/wiki/roslaunch/XML roslaunch files] that bring up the simulator in various configurations (see [[DRC/UserGuide#Launch_files|below]] for details on each launch file).

### Environment variables

The following environment variables affect the operation of DRCSim:

* `VRC_CHEATS_ENABLED`: if this variable is set to `1`, then the development aids (aka cheats) listed below in the ROS API are enabled.  Otherwise (including if the variable is not set to anything), the development aids are not enabled.
* [ROS environment variables](http://ros.org/wiki/ROS/EnvironmentVariables)
* [Gazebo environment variables](http://gazebosim.org/user_guide/started__components__env.html)

### Starting

To bring up the default DRCSim configuration (Atlas robot with no hands in an empty world):

    roslaunch drcsim_gazebo atlas.launch

For drcsim < 3.1.0: The package and launch file had a different name:

    roslaunch atlas_utils atlas.launch

### Stopping

To stop the DRCSim after having launched it with `roslaunch`, press Ctrl-C in the terminal where you executed the `roslaunch` command.  Shutting down can take several seconds; wait until you see that `roslaunch` has exited and returned to your shell prompt.

It's important to stop DRCSim in this way, by killing `roslaunch`.  If you stop it in other ways (e.g., existing from the Gazebo GUI), you might leave other processes running that can cause problems with future simulation sessions.

## Launch files

Listed below are `roslaunch` files with which users are recommended to experiment.  

Unless noted otherwise, the simulation will start with gravity disabled for 10 seconds to allow the controllers to initialize; after that gravity is enabled and the robot is standing on the ground with full dynamics.

### Launch file arguments

Unless otherwise noted, each launch file accepts the following [http://ros.org/wiki/roslaunch/Commandline%20Tools#Passing_in_args roslaunch arguments]:

* `gzname` : which executable to invoke when running Gazebo.  The default is `gazebo`, which brings up both the server and the GUI client.  Other valid values are: `gzserver`, which brings up only the server (no GUI client; useful for running on remote machines and for testing) and `gzclient`, which only brings up the GUI client (rarely useful).
* `gzworld`: which `.world` file to pass to Gazebo on startup.  The default varies with each launch file.  For example, the default world for `atlas_sandia_hands.launch` is `atlas_sandia_hands.world`.  This option is useful when you want the ROS configuration defined in a launch file but want to override the world file that's used.

E.g., to run the robot with Sandia hands without the client GUI (e.g., on a cloud machine):

    roslaunch drcsim_gazebo atlas_sandia_hands.launch gzname:=gzserver
 
For drcsim < 3.1.0: The package and launch file had a different name:

    roslaunch atlas_utils atlas_sandia_hands.launch gzname:=gzserver

### General-purpose launch files

* `drcsim_gazebo/launch/atlas.launch`.  This is the default configuration, useful for experimenting with the robot on its own.
 * Robot: Atlas with no hands
 * Environment: empty world (just ground plane)

* `drcsim_gazebo/launch/atlas_sandia_hands.launch`.  This is a simple environment that includes Atlas with the Sandia Hands.
 * Robot: Atlas with Sandia hands
 * Environment: empty world (just ground plane)

* `drcsim_gazebo/launch/atlas_drc_vehicle_fire_hose.launch`.  This environment includes Atlas, a drivable DRC Vehicle, and the standpipe for a firehose.
 * Robot: Atlas with Sandia hands
 * Environment: ground plane with drivable DRC Vehicle and firehose standpipe.
 * Tutorials: [[Tutorials/drcsim/2.0/VRC_Plugin_DRC_Vehicle | Using the VRC Plugin to tele-operate the DRC Vehicle]], [[Tutorials/drcsim/2.0/VRC_Plugin_DRC_Vehicle_With_Atlas | Using the VRC Plugin with Atlas and the DRC Vehicle]]

* `drcsim_gazebo/launch/atlas_golf_cart_fire_hose.launch`.  This environment includes Atlas, a drivable golf cart, and the standpipe for a firehose.
 * Robot: Atlas with no hands
 * Environment: ground plane with drivable golf cart and firehose standpipe.
 * Tutorials: [[Tutorials/drcsim/2.0/VRC_Plugin_Golf_Cart | Using the VRC Plugin to tele-operate the Golf Cart]], [[Tutorials/drcsim/2.0/VRC_Plugin_Golf_Cart_With_Atlas | Using the VRC Plugin with Atlas and the Golf Cart]]

* `drcsim_gazebo/launch/drc_sim_v0.launch`.  This contains a first draft of some elements of the VRC.  None of these elements are final, but may be useful for experiments.
 * Robot: Atlas with no hands
 * Environment: heightmap-based terrain, controllable golf cart, large building (power plant), hose and standpipe.

### VRC Qualification launch files

* `drcsim_gazebo/launch/qual_task_1.launch`.  The environment that will be used for VRC Qualification Task 1: walking.
 * Robot: Atlas with Sandia hands.
 * Environment: Starting pen followed by a series of gates to walk through, progressing from flat ground to steps, ramps, and small obstacles.
 (UNDER CONSTRUCTION)
* `drcsim_gazebo/launch/qual_task_2.launch`.  The environment that will be used for VRC Qualification Task 2: manipulation.
 * Robot: Atlas with Sandia hands.
 * Environment: Table with cordless drill that is to be moved into a bin.
 * Note: The robot's hip joint is pinned to the world, removing the need to balance.

* `drcsim_gazebo/launch/qual_task_3.launch`.  The environment that will be used for VRC Qualification Task 3: ??.
 * Robot: Atlas with Sandia hands.
 * Environment: ??

* `drcsim_gazebo/launch/qual_task_4.launch`.  The environment that will be used for VRC Qualification Task 4: ??.
 * Robot: Atlas with Sandia hands.
 * Environment: ??

### VRC launch files

* `drcsim_gazebo/launch/vrc_task_1.launch`.  An environment of the type that will be used for VRC Task 1: driving.
 * Robot: Atlas with Sandia hands.
 * Environment: Starting pen followed by utility vehicle that must be driven along a road.

* `drcsim_gazebo/launch/vrc_task_2.launch`.  An environment of the type that will be used for VRC Task 2: walking.
 * Robot: Atlas with Sandia hands.
 * Environment: Starting pen followed by a series of gates to walk through, progressing from flat ground increasingly challenging terrain.

* `drcsim_gazebo/launch/vrc_task_3.launch`.  An environment of the type that will be used for VRC Task 3: manipulation.
 * Robot: Atlas with Sandia hands.
 * Environment: Table with a hose that is to be connected to a spigot.

## ROS APIs

The DRC Simulation exposes a set of ROS APIs for users to develop with.  Doxygen documentation can be found in the [DRCSim API page](http://gazebosim.org/drc/api/).

### Published topics

The following data are published by the DRC Simulator.

<table>
<tr>
<td>'''Name'''</td>
<td>'''Type'''</td>
<td>'''Rate'''</td>
<td>'''Description'''</td>
</tr>

<tr><th colspan="4" align="left">System</th></tr>

<tr>
<td>/clock</td>
<td>[http://www.ros.org/doc/api/rosgraph_msgs/html/msg/Clock.html rosgraph_msgs/Clock]</td>
<td>Once per physics update, default 1000 Hz</td>
<td>The current simulation time.</td>
</tr>

<tr>
<td>/rosout</td>
<td>[http://www.ros.org/doc/api/rosgraph_msgs/html/msg/Log.html rosgraph_msgs/Log]</td>
<td>Varies</td>
<td>Log messages from various parts of the system.</td>
</tr>

<tr>
<td>/rosout_agg</td>
<td>[http://www.ros.org/doc/api/rosgraph_msgs/html/msg/Log.html rosgraph_msgs/Log]</td>
<td>Varies</td>
<td>Log messages from various parts of the system, aggregated into fewer messages for more efficient transmission.</td>
</tr>

<tr>
<td>/tf</td>
<td>[http://www.ros.org/doc/api/tf/html/msg/tfMessage.html tf/tfMessage]</td>
<td>Varies</td>
<td>Coordinate transforms from various parts of the system.  See [http://ros.org/wiki/tf the tf documentation].</td>
</tr>

<tr>
<td>/tf_static<br>/tf2_buffer_server/* </td>
<td>Various</td>
<td>Varies</td>
<td>Topics offered by <tt>tf2_buffer_server</tt>, part of [http://ros.org/wiki/tf2_ros tf2_ros]. Experimental.</td>
</tr>

<tr>
<td>/vrc_score</td>
<td>[https://bitbucket.org/osrf/drcsim/src/default/ros/atlas_msgs/msg/VRCScore.msg?at=default atlas_msgs/VRCScore]</td>
<td>1 Hz</td>
<td>Score data from the currently running task.  Only published when using VRC practice or final worlds.  <b>wall_time</b> and <b>sim_time</b> are the elapsed wall and sim time durations from the beginning of the run; the 30 minutes/run limit is enforced on the <b>sim_time</b> value.  <b>wall_time_elapsed</b> and <b>sim_time_elapsed</b> are the elapsed wall and sim time durations from when the robot passed the first gate (this event also triggers byte-counting on the router); scoring uses <b>sim_time_elapsed</b>.  This score data should be considered <i>unofficial</i>; official results will be provided by DARPA.
</td>
</tr>

<tr>
<td>/vrc/bytes/remaining/downlink<br>/vrc/bytes/remaining/uplink</td>
<td>[http://ros.org/doc/api/std_msgs/html/msg/String.html std_msgs/String]</td>
<td>1 Hz</td>
<td>How many downlink/uplink bytes remain for the currently running task.  Only published when running in the practice or competition configuration, using cloud computing resources (it's published by the <tt>vrc_netwatcher</tt>, which runs on the router).</td>
</tr>

<tr><th colspan="4" align="left">Atlas</th></tr>

<tr>
<td>/atlas/controller_statistics</td>
<td>[https://bitbucket.org/osrf/drcsim/src/default/ros/atlas_msgs/msg/ControllerStatistics.msg?at=default atlas_msgs/ControllerStatistics]</td>
<td>1 Hz</td>
<td>Timing information about the per-joint controllers, for debugging.  This message tells you the age of the command messages received on <tt>/atlas/joint_commands</tt>, where the age of a message <tt>foo</tt> is equal to (current simulation time - <tt>foo.header.timestamp</tt>).  The easiest way to make use of this debugging mechanism is to, in your ROS controller node, set <tt>header.timestamp</tt> on each outgoing command message on <tt>/atlas/joint_commands</tt> to the value of <tt>header.timestamp</tt> that was included in the most recent state message that you received on <tt>/atlas/joint_states</tt>.  Then the age data is measuring, from the per-joint controllers' perspective, the round-trip time between publishing a state message and receiving a command message that responds to that state message. See [https://bitbucket.org/osrf/drcsim/src/default/ros/atlas_msgs/pub_joint_commands.cpp an example].</td>
</tr>

<tr>
<td>/atlas/force_torque_sensors</td>
<td>[https://bitbucket.org/osrf/drcsim/src/default/atlas_msgs/msg/ForceTorqueSensors.msg atlas_msgs/ForceTorqueSensors]</td>
<td>Once per physics update, default 1000 Hz</td>
<td>Data from the force-torque sensors on the feet (3-axis: z-linear force, x and y-axis torques.  The remaining axis values are zeros.) and wrists (full 6-axis feedback).  No noise added.</td>
</tr>

<tr>
<td>/atlas/imu</td>
<td>[http://ros.org/doc/api/sensor_msgs/html/msg/Imu.html sensor_msgs/Imu]</td>
<td>Once per physics update, default 1000 Hz</td>
<td>Data from the IMU in the robot's torso.  As of DRCSim 2.2.x, no noise added.</td>
</tr>

<tr>
<td>/atlas/joint_states</td>
<td>[http://ros.org/doc/api/sensor_msgs/html/msg/JointState.html sensor_msgs/JointState]</td>
<td>Once per physics update, default 1000 Hz</td>
<td>The current state of the robot's joints (not including the sensor head or hands).  No noise added.</td>
</tr>

<tr>
<td>/atlas/atlas_state</td>
<td>[https://bitbucket.org/osrf/drcsim/raw/default/ros/atlas_msgs/msg/AtlasState.msg atlas_msgs/AtlasState]</td>
<td>Once per physics update, default 1000 Hz</td>
<td><b>Changed in DRCSim 2.3.0.</b> The current state of the robot; combines the data from <tt>/atlas/joint_states</tt>, <tt>/atlas/imu</tt>, and <tt>/atlas/force_torque_sensors</tt>.  Note that the contents of the message changed with drcsim 2.3; the changes were made to make the message smaller than 1500 bytes to accommodate transport via UDP.  Also, the topic name changed from <tt>/atlas/atlas_states</tt> to <tt>/atlas/atlas_state</tt>.</td>
</tr>

<tr>
<td>/atlas/atlas_sim_interface_state</td>
<td>[https://bitbucket.org/osrf/drcsim/raw/default/ros/atlas_msgs/msg/AtlasSimInterfaceState.msg atlas_msgs/AtlasSimInterfaceState]</td>
<td>250 Hz</td>
<td><b>New in DRCSim 2.4.0.</b> State of the BDI behavior library.</td>
</tr>

<tr>
<td>/atlas/synchronization_statistics</td>
<td>[https://bitbucket.org/osrf/drcsim/raw/default/ros/atlas_msgs/msg/SynchronizationStatistics.msg atlas_msgs/SynchronizationStatistics]</td>
<td>1000 Hz</td>
<td><b>New in DRCSim 2.6.0.</b> Data on the controller synchronization system.  Only published if the most recently received command via <tt>/atlas/atlas_command</tt> includes a non-zero value for the <tt>desired_controller_period_ms</tt> field, indicating that synchronization has been requested (see the [[Tutorials/drcsim/2.6/controller synchronization | synchronization tutorial]])</td>
</tr>

<tr><th colspan="4" align="left">Multisense-SL sensor head [1]</th></tr>

<tr>
<td>/multisense_sl/imu</td>
<td>[http://ros.org/doc/api/sensor_msgs/html/msg/Imu.html sensor_msgs/Imu]</td>
<td>Once per physics update, default 1000 Hz</td>
<td>Data from the IMU in the robot's head.  Zero-mean Gaussian noise and random bias added in DRCSim 2.3.0.</td>
</tr>

<tr>
<td>/multisense_sl/joint_states</td>
<td>[http://ros.org/doc/api/sensor_msgs/html/msg/JointState.html sensor_msgs/JointState]</td>
<td>Once per physics update, default 1000 Hz</td>
<td>The current state of the head's joint (the laser spindle).  No noise added.</td>
</tr>

<tr>
<td>/multisense_sl/laser/scan</td>
<td>[http://ros.org/doc/api/sensor_msgs/html/msg/LaserScan.html sensor_msgs/LaserScan]</td>
<td>Throttled at 40 Hz</td>
<td>Data from the laser rangefinder in the robot's head.  Zero-mean Gaussian noise added in DRCSim 2.3.0.</td>
</tr>

<tr>
<td>/multisense_sl/camera/left/image_raw</td>
<td>[http://ros.org/doc/api/sensor_msgs/html/msg/Image.html sensor_msgs/Image]</td>
<td>Default at 30Hz, adjustable between 1 to 30Hz.</td>
<td>Images from the left camera in the robot's head.  Zero-mean Gaussian noise added in DRCSim 2.3.0.</td>
</tr>

<tr>
<td>/multisense_sl/camera/left/camera_info</td>
<td>[http://ros.org/doc/api/sensor_msgs/html/msg/CameraInfo.html sensor_msgs/CameraInfo]</td>
<td>Same as corresponding /multisense_sl/camera/left/image_raw.</td>
<td>Metadata from the left camera in the robot's head.  More details on the components of the sensor_msgs/CameraInfo message can be found in [http://www.ros.org/wiki/image_pipeline/CameraInfo CameraInfo Documentation].  No noise added.</td>
</tr>


<tr>
<td>/multisense_sl/camera/right/image_raw</td>
<td>[http://ros.org/doc/api/sensor_msgs/html/msg/Image.html sensor_msgs/Image]</td>
<td>Default at 30Hz, adjustable between 1 to 30Hz.</td>
<td>Images from the right camera in the robot's head. Zero-mean Gaussian noise added in DRCSim 2.3.0.</td>
</tr>

<tr>
<td>/multisense_sl/camera/right/camera_info</td>
<td>[http://ros.org/doc/api/sensor_msgs/html/msg/CameraInfo.html sensor_msgs/CameraInfo]</td>
<td>Same as corresponding /multisense_sl/camera/right/image_raw.</td>
<td>Metadata from the right camera in the robot's head.  More details on the components of the sensor_msgs/CameraInfo message can be found in [http://www.ros.org/wiki/image_pipeline/CameraInfo CameraInfo Documentation].  No noise added.</td>
</tr>

<tr>
<td>/multisense_sl/camera/(various)</td>
<td>See [http://www.ros.org/wiki/stereo_image_proc?distro=fuerte stereo_image_proc]</td>
<td>Approximately less than 10Hz (limited by CPU load).</td>
<td>Camera data from the robot's head is fed into [http://www.ros.org/wiki/stereo_image_proc?distro=fuerte stereo_image_proc], which in turn publishes various topics.  For more details on the various parameters and topics published by the stereo_image_proc, please see [http://www.ros.org/wiki/stereo_image_proc?distro=fuerte stereo_image_proc documentation].</td>
</tr>

<tr><th colspan="4" align="left">Sandia hands</th></tr>

<tr>
<td>/sandia_hands/l_hand/joint_states</td>
<td>[http://ros.org/doc/api/sensor_msgs/html/msg/JointState.html sensor_msgs/JointState]</td>
<td>Once per physics update, default 1000 Hz</td>
<td>The current state of the joints in the robot's left hand.  No noise added.</td>
</tr>

<tr>
<td>/sandia_hands/l_hand/imu</td>
<td>[http://ros.org/doc/api/sensor_msgs/html/msg/Imu.html sensor_msgs/Imu]</td>
<td>Once per physics update, default 1000 Hz</td>
<td>Data from the IMU in the robot's left hand.  Noise and bias added in DRCSim 2.3.1.</td>
</tr>

<tr>
<td>/sandia_hands/l_hand/tactile_raw</td>
<td>[https://bitbucket.org/osrf/sandia-hand/raw/default/ros/sandia_hand_msgs/msg/RawTactile.msg sandia_hand_msgs/TactileRaw]</td>
<td>Once per physics update, default 1000 Hz</td>
<td><b>New in DRCSim 2.6.0.</b> Data from the tactile arrays in the robot's left hand. No noise added. See this [[media:Sandiahand_drc_slide.pdf‎|spec sheet]] for tactile sensor locations on the hand. TactileRaw message fields: f0: index finger, f1: middle finger, f2: little finger, f3: thumb, palm: palm. Tactile sensors on finger have an array of size 18. Index 0~5 corresponds to bottom-half of finger, and index 6~17 corresponds to top half. The output value of each sensor is within the range from 26500 to 33500. The lower bound, 26500, means zero or minimal force feedback.</td>
</tr>

<tr>
<td>/sandia_hands/l_hand/camera/left/image_raw</td>
<td>[http://ros.org/doc/api/sensor_msgs/html/msg/Image.html sensor_msgs/Image]</td>
<td>Default at 30Hz, not adjustable.</td>
<td><b>New in DRCSim 2.3.0.</b> Images from the right camera in the robot's left hand.  Zero-mean Gaussian noise added.</td>
</tr>

<tr>
<td>/sandia_hands/l_hand/camera/left/camera_info</td>
<td>[http://ros.org/doc/api/sensor_msgs/html/msg/CameraInfo.html sensor_msgs/CameraInfo]</td>
<td>Same as corresponding image topic (/sandia_hands/l_hand/camera/left/image_raw)</td>
<td><b>New in DRCSim 2.3.0.</b> Metadata from the right camera in the robot's left hand.  More details on the components of the sensor_msgs/CameraInfo message can be found in [http://www.ros.org/wiki/image_pipeline/CameraInfo CameraInfo Documentation].</td>
</tr>

<tr>
<td>/sandia_hands/l_hand/camera/right/image_raw</td>
<td>[http://ros.org/doc/api/sensor_msgs/html/msg/Image.html sensor_msgs/Image]</td>
<td>Default at 30Hz, not adjustable.</td>
<td><b>New in DRCSim 2.3.0.</b> Images from the right camera in the robot's right hand.  Zero-mean Gaussian noise added.</td>
</tr>

<tr>
<td>/sandia_hands/l_hand/camera/right/camera_info</td>
<td>[http://ros.org/doc/api/sensor_msgs/html/msg/CameraInfo.html sensor_msgs/CameraInfo]</td>
<td>Same as corresponding image topic (/sandia_hands/l_hand/camera/right/image_raw)</td>
<td><b>New in DRCSim 2.3.0.</b> Metadata from the right camera in the robot's right hand  More details on the components of the sensor_msgs/CameraInfo message can be found in [http://www.ros.org/wiki/image_pipeline/CameraInfo CameraInfo Documentation].</td>
</tr>

<tr>
<td>/sandia_hands/l_hand/camera/(various)</td>
<td>See [http://www.ros.org/wiki/stereo_image_proc?distro=fuerte stereo_image_proc]</td>
<td>Approximately less than 10Hz (limited by CPU load).</td>
<td><b>New in DRCSim 2.3.1.</b> Camera data from the robot's left hand is fed into
[http://www.ros.org/wiki/stereo_image_proc?distro=fuerte stereo_image_proc], which in turn publishes various topics</td>
</tr>

<tr>
<td>/sandia_hands/r_hand/joint_states</td>
<td>[http://ros.org/doc/api/sensor_msgs/html/msg/JointState.html sensor_msgs/JointState]</td>
<td>Once per physics update, default 1000 Hz</td>
<td>The current state of the joints in the robot's right hand.  No noise added.</td>
</tr>

<tr>
<td>/sandia_hands/r_hand/imu</td>
<td>[http://ros.org/doc/api/sensor_msgs/html/msg/Imu.html sensor_msgs/Imu]</td>
<td>Once per physics update, default 1000 Hz</td>
<td>Data from the IMU in the robot's right hand.  Noise and bias added in DRCSim 2.3.1.</td>
</tr>

<tr>
<td>/sandia_hands/r_hand/tactile_raw</td>
<td>[https://bitbucket.org/osrf/sandia-hand/raw/default/ros/sandia_hand_msgs/msg/RawTactile.msg sandia_hand_msgs/TactileRaw]</td>
<td>Once per physics update, default 1000 Hz</td>
<td><b>New in DRCSim 2.6.0.</b> Data from the tactile arrays in the robot's right hand. No noise added. See this [[media:Sandiahand_drc_slide.pdf‎|spec sheet]] for tactile sensor locations on the hand. TactileRaw message fields: f0: index finger, f1: middle finger, f2: little finger, f3: thumb, palm: palm. Tactile sensors on finger have an array of size 18. Index 0~5 corresponds to bottom-half of finger, and index 6~17 corresponds to top half. The output value of each sensor is within the range from 26500 to 33500. The lower bound, 26500, means zero or minimal force feedback.</td>
</tr>

<tr>
<td>/sandia_hands/r_hand/camera/left/image_raw</td>
<td>[http://ros.org/doc/api/sensor_msgs/html/msg/Image.html sensor_msgs/Image]</td>
<td>Default at 30Hz, not adjustable.</td>
<td><b>New in DRCSim 2.3.0.</b> Images from the right camera in the robot's right hand.  Zero-mean Gaussian noise added.</td>
</tr>

<tr>
<td>/sandia_hands/r_hand/camera/left/camera_info</td>
<td>[http://ros.org/doc/api/sensor_msgs/html/msg/CameraInfo.html sensor_msgs/CameraInfo]</td>
<td>Same as corresponding image topic (/sandia_hands/r_hand/camera/left/image_raw)</td>
<td><b>New in DRCSim 2.3.0.</b> Metadata from the left camera in the robot's right hand.  More details on the components of the sensor_msgs/CameraInfo message can be found in [http://www.ros.org/wiki/image_pipeline/CameraInfo CameraInfo Documentation].</td>
</tr>

<tr>
<td>/sandia_hands/r_hand/camera/right/image_raw</td>
<td>[http://ros.org/doc/api/sensor_msgs/html/msg/Image.html sensor_msgs/Image]</td>
<td>Default at 30Hz, not adjustable.</td>
<td><b>New in DRCSim 2.3.0.</b> Images from the right camera in the robot's right hand.  Zero-mean Gaussian noise added.</td>
</tr>

<tr>
<td>/sandia_hands/r_hand/camera/right/camera_info</td>
<td>[http://ros.org/doc/api/sensor_msgs/html/msg/CameraInfo.html sensor_msgs/CameraInfo]</td>
<td>Same as corresponding image topic (/sandia_hands/r_hand/camera/right/image_raw)</td>
<td><b>New in DRCSim 2.3.0.</b> Metadata from the right camera in the robot's right hand  More details on the components of the sensor_msgs/CameraInfo message can be found in [http://www.ros.org/wiki/image_pipeline/CameraInfo CameraInfo Documentation].</td>
</tr>

<tr>
<td>/sandia_hands/r_hand/camera/(various)</td>
<td>See [http://www.ros.org/wiki/stereo_image_proc?distro=fuerte stereo_image_proc]</td>
<td>Approximately less than 10Hz (limited by CPU load).</td>
<td><b>New in DRCSim 2.3.1.</b> Camera data from the robot's right hand is fed into
[http://www.ros.org/wiki/stereo_image_proc?distro=fuerte stereo_image_proc], which in turn publishes various topics</td>
</tr>

<tr><th colspan="4" align="left">Development aids (not available during competition)</th></tr>

<tr>
<td>/atlas/debug/l_foot_contact,<br>/atlas/debug/r_foot_contact</td>
<td>[http://ros.org/doc/api/geometry_msgs/html/msg/WrenchStamped.html geometry_msgs/WrenchStamped]</td>
<td>Once per physics update, default 1000 Hz</td>
<td>Contact forces and torques on the left foot (l_foot_contact) and right foot (r_foot_contact) of Atlas</td>
</tr>

<tr>
<td>/drc_vehicle/brake_pedal/state,<br>/golf_cart/brake_pedal/state</td>
<td>[http://ros.org/doc/api/std_msgs/html/msg/Float64.html std_msgs/Float64]</td>
<td>20 Hz (set in ros/atlas_msgs/ DRCVehicleROSPlugin.cpp)</td>
<td>Current brake pedal state from 0 (no brake applied) to 1.0 (100% braking applied). See the [[Tutorials/drcsim/2.0/VRC_Plugin_DRC_Vehicle|drc_vehicle tutorial]] and [[Tutorials/drcsim/2.0/VRC_Plugin_Golf_Cart|golf_cart tutorial]].</td>
</tr>

<tr>
<td>/drc_vehicle/direction/state,<br>/golf_cart/direction/state</td>
<td>[http://ros.org/doc/api/std_msgs/html/msg/Int8.html std_msgs/Int8]</td>
<td>20 Hz (set in ros/atlas_msgs/ DRCVehicleROSPlugin.cpp)</td>
<td>Current state of direction switch with -1: Reverse, 0: Neutral, 1: Forward. See the [[Tutorials/drcsim/2.0/VRC_Plugin_DRC_Vehicle|drc_vehicle tutorial]] and [[Tutorials/drcsim/2.0/VRC_Plugin_Golf_Cart|golf_cart tutorial]].</td>
</tr>

<tr>
<td>/drc_vehicle/gas_pedal/state,<br>/golf_cart/gas_pedal/state</td>
<td>[http://ros.org/doc/api/std_msgs/html/msg/Float64.html std_msgs/Float64]</td>
<td>20 Hz (set in ros/atlas_msgs/ DRCVehicleROSPlugin.cpp)</td>
<td>Current gas pedal state from 0 (no gas applied) to 1.0 (100% gas applied). See the [[Tutorials/drcsim/2.0/VRC_Plugin_DRC_Vehicle|drc_vehicle tutorial]] and [[Tutorials/drcsim/2.0/VRC_Plugin_Golf_Cart|golf_cart tutorial]].</td>
</tr>

<tr>
<td>/drc_vehicle/hand_brake/state,<br>/golf_cart/hand_brake/state</td>
<td>[http://ros.org/doc/api/std_msgs/html/msg/Float64.html std_msgs/Float64]</td>
<td>20 Hz (set in ros/atlas_msgs/ DRCVehicleROSPlugin.cpp)</td>
<td>Current hand brake state from 0 (no brake applied) to 1.0 (100% braking applied). See the [[Tutorials/drcsim/2.0/VRC_Plugin_DRC_Vehicle|drc_vehicle tutorial]] and [[Tutorials/drcsim/2.0/VRC_Plugin_Golf_Cart|golf_cart tutorial]].</td>
</tr>

<tr>
<td>/drc_vehicle/hand_wheel/state,<br>/golf_cart/hand_wheel/state</td>
<td>[http://ros.org/doc/api/std_msgs/html/msg/Float64.html std_msgs/Float64]</td>
<td>20 Hz (set in ros/atlas_msgs/ DRCVehicleROSPlugin.cpp)</td>
<td>Current angle of the steering hand wheel in radians. See the [[Tutorials/drcsim/2.0/VRC_Plugin_DRC_Vehicle|drc_vehicle tutorial]] and [[Tutorials/drcsim/2.0/VRC_Plugin_Golf_Cart|golf_cart tutorial]].</td>
</tr>

<tr>
<td>/drc_vehicle/key/state,<br>/golf_cart/key/state</td>
<td>[http://ros.org/doc/api/std_msgs/html/msg/Int8.html std_msgs/Int8]</td>
<td>20 Hz (set in ros/atlas_msgs/ DRCVehicleROSPlugin.cpp)</td>
<td>Current state of key switch with 0: Off, 1: On, -1: Error state requiring direction switch to be placed in Neutral before gas torque can be applied. See the [[Tutorials/drcsim/2.0/VRC_Plugin_DRC_Vehicle|drc_vehicle tutorial]] and [[Tutorials/drcsim/2.0/VRC_Plugin_Golf_Cart|golf_cart tutorial]].</td>
</tr>

<tr>
<td>/ground_truth_odom</td>
<td>[http://ros.org/doc/api/nav_msgs/html/msg/Odometry.html nav_msgs/Odometry]</td>
<td>100 Hz (specified in ros/atlas_description /urdf/atlas.gazebo)</td>
<td>Ground truth pose of atlas pelvis.</td>
</tr>

</table>

Notes:

 * [1] The physical Multisense-SL device has some limitations regarding how many streams of data it can provide simultaneously due to available network bandwidth.  drcsim does not implement the corresponding logic to provide matching behavior.  If you want to ensure that your code will transfer directly to hardware, you should live within the constraints of the hardware when working in simulation.  Having said that, it is likely that drcsim will provide smaller images, at a lower frame rate than the physical device because of CPU limitations in stereo processing (the physical device does stereo in an FPGA and so does not suffer from this limitation).

### Subscribed topics

The following commands are subscribed by the DRC Simulator.

<table>
<tr>
<td>'''Name'''</td>
<td>'''Type'''</td>
<td>'''Description'''</td>
</tr>

<tr><th colspan="3" align="left">Atlas</th></tr>

<tr>
<td>/atlas/control_mode</td>
<td>[http://ros.org/doc/api/std_msgs/html/msg/String.html std_msgs/String]</td>
<td>Control mode for Boston Dynamics Behavior Library ([https://bitbucket.org/osrf/drcsim/src/default/plugins/AtlasSimInterface_1.0.3/doc/html/classAtlasSimInterface.html?at=default#cl-189 copied from documentation here])
<ul>
<li>"User" - no control from behavior; all values set by performer</li>
<li>"Stand" - simple stand behavior; some values set by behavior</li>
<li>"Walk" - simple walk behavior; some values set by behavior</li>
<li>"Safety" - joint position hold</li>
<li>"StandPrep - stance pose joint position hold</li>
</ul>
'''NOTE''' This mode will be limited, please use the `/atlas/atlas_sim_interface_command` and `/atlas/atlas_sim_interface_state` topics for interfacing with Boston Dynamics Behavior Library.
</td>
</tr>

<tr>
<td>/atlas/atlas_command</td>
<td>[https://bitbucket.org/osrf/drcsim/src/default/ros/atlas_msgs/msg/AtlasCommand.msg?at=default atlas_msgs/AtlasCommand]</td>
<td><b>New in DRCSim 2.3.0.</b> Command data to the Atlas robot. No noise added. This topic, instead of `/atlas/joint_commands`, is recommended for use by controllers that wish to operate at a higher update rate with simulation.  It is specifically designed to be less than 1500 bytes, so as to be amenable to transport via UDP.</td>
</tr>

<tr>
<td>/atlas/atlas_sim_interface_command</td>
<td>[https://bitbucket.org/osrf/drcsim/src/default/ros/atlas_msgs/msg/AtlasSimInterfaceCommand.msg?at=default atlas_msgs/AtlasSimInterfaceCommand]</td>
<td><b>New in DRCSim 2.4.0.</b> Interface to send commands to the BDI behavior library.</td>
</tr>

<tr>
<td>/atlas/joint_commands</td>
<td>[https://bitbucket.org/osrf/osrf-common/raw/default/ros/osrf_msgs/msg/JointCommands.msg osrf_msgs/JointCommands]</td>
<td>Setpoints and gains for the robot's joints (not including the sensor head or hands), see [[Tutorials/drcsim/2.2/sending_joint_controller_commands_over_ros | Atlas control tutorial with C++]] and [[Tutorials/drcsim/2.2/Atlas_control_over_ROS_topics_with_python | Atlas control tutorial with python]].</td>
</tr>

<tr><th colspan="3" align="left">Multisense-SL sensor head</th></tr>

<tr>
<td>/multisense_sl/set_spindle_speed</td>
<td>[http://ros.org/doc/api/std_msgs/html/msg/Float64.html std_msgs/Float64]</td>
<td>Desired velocity, in radians/second, of the spindle holding the laser rangefinder (set to 0 to stop rotation)</td>
</tr>

<tr>
<td>/multisense_sl/fps</td>
<td>[http://ros.org/doc/api/std_msgs/html/msg/Float64.html std_msgs/Float64]</td>
<td><b>Not yet implemented</b>. Desired image capture rate, in frames per second.</td>
</tr>

<tr><th colspan="3" align="left">Sandia hands</th></tr>

<tr>
<td>/sandia_hands/l_hand/joint_commands<br>/sandia_hands/r_hand/joint_commands</td>
<td>[https://bitbucket.org/osrf/osrf-common/raw/default/ros/osrf_msgs/msg/JointCommands.msg osrf_msgs/JointCommands]</td>
<td>Setpoints and gains for the joints in the robot's left hand (l_hand) and right hand (r_hand)</td>
</tr>

<tr>
<td>/sandia_hands/l_hand/simple_grasp<br>/sandia_hands/r_hand/simple_grasp</td>
<td>[https://bitbucket.org/osrf/sandia-hand/raw/default/ros/sandia_hand_msgs/msg/SimpleGrasp.msg sandia_hand_msgs/SimpleGrasp]</td>
<td>Command simple grasps to left hand (l_hand) and right hand (r_hand).  Valid values for the <tt>name</tt> field are: <tt>"cylindrical"</tt>, <tt>"spherical"</tt>, and <tt>"prismatic"</tt>.  No guarantees are provided about the capabilities of these grasps.</td>
</tr>

<tr><th colspan="3" align="left">Development aids (not available during competition)</th></tr>

<tr>
<td>/atlas/cmd_vel</td>
<td>[http://ros.org/doc/api/geometry_msgs/html/msg/Twist.html geometry_msgs/Twist]</td>
<td>Move atlas around as if it were wheeled robot, without walking or balancing ([[Tutorials/drcsim/2.0/fake_walking_teleop | see this tutorial]])</td>
</tr>

<tr>
<td>/atlas/configuration</td>
<td>[http://ros.org/doc/api/sensor_msgs/html/msg/JointState.html sensor_msgs/JointState]</td>
<td>Not currently implemented.</td>
</tr>

<tr>
<td>/atlas/set_pose</td>
<td>[http://ros.org/doc/api/geometry_msgs/html/msg/Pose.html geometry_msgs/Pose]</td>
<td>Teleport the robot with the current configuration to the desired pose (relative to the pelvis). For example, `rostopic pub /atlas/set_pose --once 'geometry_msgs/Pose' '{position: {z: 0.95}, orientation: {w: 1}}'` will return the robot approximately to the starting point.</td>
</tr>

<tr>
<td>/joint_trajectory</td>
<td>[http://ros.org/doc/api/trajectory_msgs/html/msg/JointTrajectory.html trajectory_msgs/JointTrajectory]</td>
<td>Disables physics and animates a robot by playing back a joint trajectory ([[Tutorials/drcsim/2.0/ros_animated_robot |see tutorial]]).</td>
</tr>

<tr>
<td>/atlas/mode</td>
<td>[http://ros.org/doc/api/std_msgs/html/msg/String.html std_msgs/String]</td>
<td>Set atlas mode: "nominal" (normal), "no_gravity" (robot floats), "pinned" (pin the hip joint to the world, turn off gravity), "pinned_with_gravity" (pin the hip, turn on gravity), "feet" (pin the feet to the ground), "harnessed" (similar to "pinned").</td>
</tr>

<tr>
<td>/atlas/debug/test</td>
<td>[https://bitbucket.org/osrf/drcsim/raw/default/ros/atlas_msgs/msg/Test.msg atlas_msgs/Test]</td>/tmp/qual_task_1
<td>For internal testing.  Do not use.</td>
</tr>

<tr>
<td>/atlas/debug/sync_delay</td>
<td>[http://ros.org/doc/api/std_msgs/html/msg/String.html std_msgs/String]</td>
<td>For internal testing.  Do not use.</td>
</tr>

<tr>
<td>/atlas/apply_pelvis_force</td>
<td>[http://ros.org/doc/api/geometry_msgs/html/msg/Wrench.html geometry_msgs/Wrench]</td>
<td><b>New in 2.4.0.</b> Apply a force to the pelvis.</td>
</tr>

<tr>
<td>/atlas/pause</td>
<td>[http://ros.org/doc/api/std_msgs/html/msg/String.html std_msgs/String]</td>
<td><b>New in 2.4.0.</b> For internal testing.  Do not use.</td>
</tr>

<tr>
<td>/drc_world/robot_enter_car</td>
<td>[http://ros.org/doc/api/geometry_msgs/html/msg/Pose.html geometry_msgs/Pose]</td>
<td>Teleport and pin the robot to the driver's seat of the Golf Cart or DRC Vehicle if the appropriate world is loaded. The pose specifies an offset from the default seated position. See the [[Tutorials/drcsim/2.0/VRC_Plugin_Golf_Cart_With_Atlas | Golf Cart with Atlas tutorial]] and the [[Tutorials/drcsim/2.0/VRC_Plugin_DRC_Vehicle_With_Atlas | DRC Vehicle with Atlas tutorial]].</td>
</tr>

<tr>
<td>/drc_world/robot_exit_car</td>
<td>[http://ros.org/doc/api/geometry_msgs/html/msg/Pose.html geometry_msgs/Pose]</td>
<td>Unpin the robot from the driver's seat and teleport to the driver's side door of the Golf Cart or DRC Vehicle if the appropriate world is loaded. The pose specifies an offset from the default location near the driver's side door. See the [[Tutorials/drcsim/2.0/VRC_Plugin_Golf_Cart_With_Atlas | Golf Cart with Atlas tutorial]] and the [[Tutorials/drcsim/2.0/VRC_Plugin_DRC_Vehicle_With_Atlas | DRC Vehicle with Atlas tutorial]].</td>
</tr>

<tr>
<td>/drc_world/robot_grab_link</td>
<td>[http://ros.org/doc/api/geometry_msgs/html/msg/Pose.html geometry_msgs/Pose]</td>
<td>Pin the fire hose link to the right hand of atlas if the appropriate world is loaded. The pose argument is currently ignored.</td>
</tr>

<tr>
<td>/drc_world/robot_release_link</td>
<td>[http://ros.org/doc/api/geometry_msgs/html/msg/Pose.html geometry_msgs/Pose]</td>
<td>Unpin the fire hose link from the right hand of atlas if the appropriate world is loaded. The pose argument is currently ignored.</td>
</tr>

<tr>
<td>/drc_vehicle/brake_pedal/cmd<br>/golf_cart/brake_pedal/cmd</td>
<td>[http://ros.org/doc/api/std_msgs/html/msg/Float64.html std_msgs/Float64]</td>
<td>Set brake pedal command from 0 (no brake applied) to 1.0 (100% braking applied). See the [[Tutorials/drcsim/2.0/VRC_Plugin_DRC_Vehicle|drc_vehicle tutorial]] and [[Tutorials/drcsim/2.0/VRC_Plugin_Golf_Cart|golf_cart tutorial]].</td>
</tr>

<tr>
<td>/drc_vehicle/direction/cmd<br>/golf_cart/direction/cmd</td>
<td>[http://ros.org/doc/api/std_msgs/html/msg/Int8.html std_msgs/Int8]</td>
<td>Set direction switch with -1: Reverse, 0: Neutral, 1: Forward. Direction switch defaults to Forward. See the [[Tutorials/drcsim/2.0/VRC_Plugin_DRC_Vehicle|drc_vehicle tutorial]] and [[Tutorials/drcsim/2.0/VRC_Plugin_Golf_Cart|golf_cart tutorial]].</td>
</tr>

<tr>
<td>/drc_vehicle/gas_pedal/cmd<br>/golf_cart/gas_pedal/cmd</td>
<td>[http://ros.org/doc/api/std_msgs/html/msg/Float64.html std_msgs/Float64]</td>
<td>Set gas pedal command from 0 (no gas applied) to 1.0 (100% gas applied). See the [[Tutorials/drcsim/2.0/VRC_Plugin_DRC_Vehicle|drc_vehicle tutorial]] and [[Tutorials/drcsim/2.0/VRC_Plugin_Golf_Cart|golf_cart tutorial]].</td>
</tr>

<tr>
<td>/drc_vehicle/hand_brake/cmd<br>/golf_cart/hand_brake/cmd</td>
<td>[http://ros.org/doc/api/std_msgs/html/msg/Float64.html std_msgs/Float64]</td>
<td>Set hand brake command from 0 (no brake applied) to 1.0 (100% braking applied). See the [[Tutorials/drcsim/2.0/VRC_Plugin_DRC_Vehicle|drc_vehicle tutorial]] and [[Tutorials/drcsim/2.0/VRC_Plugin_Golf_Cart|golf_cart tutorial]].</td>
</tr>

<tr>
<td>/drc_vehicle/hand_wheel/cmd<br>/golf_cart/hand_wheel/cmd</td>
<td>[http://ros.org/doc/api/std_msgs/html/msg/Float64.html std_msgs/Float64]</td>
<td>Set desired angle of the steering hand wheel in radians. See the [[Tutorials/drcsim/2.0/VRC_Plugin_DRC_Vehicle|drc_vehicle tutorial]] and [[Tutorials/drcsim/2.0/VRC_Plugin_Golf_Cart|golf_cart tutorial]].</td>
</tr>

<tr>
<td>/drc_vehicle/key/cmd<br>/golf_cart/key/cmd</td>
<td>[http://ros.org/doc/api/std_msgs/html/msg/Int8.html std_msgs/Int8]</td>
<td>Set key switch with 0: Off, 1: On. Note that the direction switch must be in Neutral when the key is turned on or an error will result. The key defaults to On. '''This development aid is currently the only way to set the key switch of the vehicle.''' See the [[Tutorials/drcsim/2.0/VRC_Plugin_DRC_Vehicle|drc_vehicle tutorial]] and [[Tutorials/drcsim/2.0/VRC_Plugin_Golf_Cart|golf_cart tutorial]].</td>
</tr>

</table>


### ROS Services

The following ROS services are subscribed to by the DRC Simulator.

<table>
<tr>
<td>'''Name'''</td>
<td>'''Type'''</td>
<td>'''Description'''</td>
</tr>

<tr><th colspan="3" align="left">Atlas</th></tr>

<tr>
<td>/atlas/reset_controls</td>
<td>[https://bitbucket.org/osrf/drcsim/src/default/ros/atlas_msgs/srv/ResetControls.srv?at=default atlas_msgs/ResetControls]</td>
<td>Reset various parts of the controllers' internal state.</td>
</tr>

<tr>
<td>/atlas/set_joint_damping</td>
<td>[https://bitbucket.org/osrf/drcsim/src/default/ros/atlas_msgs/srv/SetJointDamping.srv?at=default atlas_msgs/SetJointDamping]</td>
<td><b>New in DRCSim 2.6.0.</b> Set viscous joint damping coefficients for Atlas.  Input array damping_coefficients must have 28 elements, one per joint, and the order of joints can be found [https://bitbucket.org/osrf/drcsim/src/default/ros/atlas_msgs/msg/AtlasState.msg?at=default#cl-14 in atlas_msgs/AtlasState].  Damping coefficient limits and default values for each joint are listed below:
<table>
<tr><td>Joint Name</td><td>Min(Nms/rad)</td><td>Max(Nms/rad)</td><td>Default(Nms/rad)</td></tr>
<tr><th colspan="4" align="left"></th></tr>
<tr><td>back_lbz</td><td>0.100000</td><td>516.733333</td><td>10.000000</td></tr>
<tr><td>back_mby</td><td>0.100000</td><td>861.845833</td><td>10.000000</td></tr>
<tr><td>back_ubx</td><td>0.100000</td><td>395.458333</td><td>10.000000</td></tr>
<tr><td>neck_ay</td><td>0.100000</td><td>20.833333</td><td>1.000000</td></tr>
<tr><td>l_leg_uhz</td><td>0.100000</td><td>458.333333</td><td>1.000000</td></tr>
<tr><td>l_leg_mhx</td><td>0.100000</td><td>750.000000</td><td>1.000000</td></tr>
<tr><td>l_leg_lhy</td><td>0.100000</td><td>1083.333333</td><td>1.000000</td></tr>
<tr><td>l_leg_kny</td><td>0.100000</td><td>1666.666667</td><td>1.000000</td></tr>
<tr><td>l_leg_uay</td><td>0.100000</td><td>916.666667</td><td>1.000000</td></tr>
<tr><td>l_leg_lax</td><td>0.100000</td><td>375.000000</td><td>1.000000</td></tr>
<tr><td>r_leg_uhz</td><td>0.100000</td><td>1083.333333</td><td>1.000000</td></tr>
<tr><td>r_leg_mhx</td><td>0.100000</td><td>750.000000</td><td>1.000000</td></tr>
<tr><td>r_leg_lhy</td><td>0.100000</td><td>1083.333333</td><td>1.000000</td></tr>
<tr><td>r_leg_kny</td><td>0.100000</td><td>1666.666667</td><td>1.000000</td></tr>
<tr><td>r_leg_uay</td><td>0.100000</td><td>916.666667</td><td>1.000000</td></tr>
<tr><td>r_leg_lax</td><td>0.100000</td><td>375.000000</td><td>1.000000</td></tr>
<tr><td>l_arm_usy</td><td>0.100000</td><td>883.333333</td><td>1.000000</td></tr>
<tr><td>l_arm_shx</td><td>0.100000</td><td>708.333333</td><td>1.000000</td></tr>
<tr><td>l_arm_ely</td><td>0.100000</td><td>475.000000</td><td>1.000000</td></tr>
<tr><td>l_arm_elx</td><td>0.100000</td><td>475.000000</td><td>1.000000</td></tr>
<tr><td>l_arm_uwy</td><td>0.100000</td><td>475.000000</td><td>1.000000</td></tr>
<tr><td>l_arm_mwx</td><td>0.100000</td><td>250.000000</td><td>1.000000</td></tr>
<tr><td>r_arm_usy</td><td>0.100000</td><td>883.333333</td><td>1.000000</td></tr>
<tr><td>r_arm_shx</td><td>0.100000</td><td>708.333333</td><td>1.000000</td></tr>
<tr><td>r_arm_ely</td><td>0.100000</td><td>475.000000</td><td>1.000000</td></tr>
<tr><td>r_arm_elx</td><td>0.100000</td><td>475.000000</td><td>1.000000</td></tr>
<tr><td>r_arm_uwy</td><td>0.100000</td><td>475.000000</td><td>1.000000</td></tr>
<tr><td>r_arm_mwx</td><td>0.100000</td><td>250.000000</td><td>1.000000</td></tr>
</table>
</td>
</tr>

<tr>
<td>/atlas/get_joint_damping</td>
<td>[https://bitbucket.org/osrf/drcsim/src/default/ros/atlas_msgs/srv/GetJointDamping.srv?at=default atlas_msgs/GetJointDamping]</td>
<td><b>New in DRCSim 2.6.0.</b> Get viscous joint damping coefficients for Atlas.   Resulting array of damping_coefficients has 28 elements, one per joint, and the order of joints can be found [https://bitbucket.org/osrf/drcsim/src/default/ros/atlas_msgs/msg/AtlasState.msg?at=default#cl-14 in atlas_msgs/AtlasState]</td>
</tr>

<tr>
<td>/atlas/atlas_filters</td>
<td>[https://bitbucket.org/osrf/drcsim/src/default/ros/atlas_msgs/srv/AtlasFilters.srv?at=default atlas_msgs/AtlasFilters]</td>
<td><b>New in DRCSim 2.6.0.</b>  Control position and/or velocity filtering (implemented in a plugin running inside simulation at 1KHz).</td>
</tr>

<tr><th colspan="3" align="left">Multisense-SL sensor head</th></tr>

<tr>
<td>/multisense_sl/camera/(various)</td>
<td>See [http://www.ros.org/wiki/stereo_image_proc?distro=fuerte stereo_image_proc]</td>
<td>Various <a href="http://ros.org/wiki/dynamic_reconfigure">dynamic_reconfigure</a> services are provided to allow configuration of stereo image processing. For more details on the various parameters and services offered by the stereo_image_proc, please see [http://www.ros.org/wiki/stereo_image_proc?distro=fuerte stereo_image_proc documentation].</td>
</tr>

<tr><th colspan="3" align="left">Sandia hands</th></tr>

<tr>
<td>/sandia_hands/set_joint_damping</td>
<td>[https://bitbucket.org/osrf/drcsim/src/default/ros/atlas_msgs/srv/SetJointDamping.srv?at=default atlas_msgs/SetJointDamping]</td>
<td>Set viscous joint damping coefficients for both robot's left hand (l_hand) and right hand (r_hand).   The first 24 of the 28 element-long input array damping_coefficients are used, one per joint, and the order of joints can be found [https://bitbucket.org/osrf/drcsim/src/6a67bc157da6/ros/atlas_msgs/SandiaHandPlugin.cpp?at=default#cl-65 here].  Joint damping coefficients can be in the range of 1.0 Nms/rad to 30.0 Nms/rad.</td>
</tr>

<tr>
<td>/sandia_hands/get_joint_damping</td>
<td>[https://bitbucket.org/osrf/drcsim/src/default/ros/atlas_msgs/srv/GetJointDamping.srv?at=default atlas_msgs/GetJointDamping]</td>
<td>Get viscous joint damping coefficients for both robot's left hand (l_hand) and right hand (r_hand).   The first 24 of the 28 element-long damping_coefficients will be filled, one per joint, and the order of joints can be found [https://bitbucket.org/osrf/drcsim/src/6a67bc157da6/ros/atlas_msgs/SandiaHandPlugin.cpp?at=default#cl-65 here].</td>
</tr>

<tr>
<td>/sandia_hands/l_hand/simple_grasp<br>/sandia_hands/r_hand/simple_grasp</td>
<td>[https://bitbucket.org/osrf/sandia-hand/src/default/ros/sandia_hand_msgs/srv/SimpleGraspSrv.srv?at=default sandia_hand_msgs/SimpleGraspSrv]</td>
<td>Command simple grasps to left hand (l_hand) and right hand (r_hand).  Valid values for the <tt>name</tt> field are: <tt>"cylindrical"</tt>, <tt>"spherical"</tt>, and <tt>"prismatic"</tt>.  No guarantees are provided about the capabilities of these grasps.</td>
</tr>

<tr><th colspan="3" align="left">Development aids (not available during competition)</th></tr>

<tr>
<td>/gazebo/pause_physics</td>
<td>[http://ros.org/doc/api/std_msgs/html/msg/Empty.html std_msgs/Empty]</td>
<td>Pauses Gazebo.</td>
</tr>

<tr>
<td>/gazebo/unpause_physics</td>
<td>[http://ros.org/doc/api/std_msgs/html/msg/Empty.html std_msgs/Empty]</td>
<td>Unpauses Gazebo.</td>
</tr>

<tr>
<td>/gazebo/reset_simulation</td>
<td>[http://ros.org/doc/api/std_msgs/html/msg/Empty.html std_msgs/Empty]</td>
<td>Resets simulation.</td>
</tr>

<tr>
<td>/gazebo/reset_models</td>
<td>[http://ros.org/doc/api/std_msgs/html/msg/Empty.html std_msgs/Empty]</td>
<td>Resets model poses in Gazebo.</td>
</tr>


</table>


### Controllers
**Note: Under construction, details may change drastically in the next few iterations.**

#### Atlas Per-Joint Servo Controllers

At the lowest level, on every simulation update at 1kHz, joint torque is computed based on the following formula:
~~~
effort_commanded =
 k_effort * (
   kp_position     * ( position - measured_position )       +
   ki_position     * 1/s * ( position - measured_position ) +
   kd_position     * s * ( position - measured_position ) +
   kp_velocity     * ( velocity - measured_velocity )     +
   effort ) +
 (1 - k_effort) * effort_bdi_controller
~~~
Note that the `kp_velocity` term is subject to special treatment that is detailed in the following section.

#### High Bandwidth Joint Velocity Implicit Damping via kp_velocity

A high bandwidth viscous damping mechanism is provided to mitigate the noise in joint velocity measurements. The viscous damping coefficient at each Atlas joint can be set by the `kp_velocity` gain in the AtlasCommand message and is passed to the ODE solver as an implicit damping coefficient, which improves controller stability. The `kp_velocity` gain will be truncated to the range specified in [ROS service section](http://gazebosim.org/w/index.php?title=DRC/UserGuide#ROS_Services). Further details on the implementation can be seen in the source code [AtlasPlugin.cpp:2360-2436](https://bitbucket.org/osrf/drcsim/src/aec75e352ee235254441b5cb9b870a7c67bc68d1/ros/atlas_msgs/AtlasPlugin.cpp?at=drcsim_2.6#cl-2360).

#### Boston Dynamics Atlas Simulation Behavior Library (AtlasSimInterface)

The AtlasSimInterface library populates the feed-forward force command (`effort_bdi_controller`) in the per-joint controllers.  See [Controller ROS API section](http://gazebosim.org/wiki/DRC/UserGuide#Controller_ROS_API) for hooks to call into the behavior library.

Updates regarding release state and available behaviors will be detailed in the [ChangeLog](http://gazebosim.org/wiki/DRC/Change_log) and [RoadMap](http://gazebosim.org/wiki/DRC/Roadmap).

There is some initial [API documentation](http://gazebosim.org/drc/api/atlas_interface/index.html) for the underlying behavior library.  The ROS interface is a pretty thin wrapper around the C++ library API.

##### AtlasSimInterface Behaviors

Behaviors are controller states that govern which joints are controller-governed, and which are user-governed. The neck joint, unless otherwise stated, is user-controlled.

Behavior changes are controlled by publishing to the 'atlas_sim_interface_command' topic, or are controlled automatically. Examples of automatic changes include switching to Freeze when the robot starts to fall or reverting to stand if enough steps weren't provided in the walk behavior. Sometimes, a requested behavior will not be possible as determined by the controller and will be ignored.

  * **User**: All joints controlled by performer (through the per-joint servo controllers).
  * **Stand**: Statically stable stand.  This is the "hub" mode, entry and termination into other behaviors.
  * **Walk**: Dynamically stable walking using approximate step
locations.
  * **Step**: Slow walking with precise step locations, statically stable
between steps.
  * **Manipulate**: Statically stable stand, but with upper body joints
available for performer control to enable tool use and environment
interaction.
  * **Freeze**: For falling, when other behaviors have no chance of
working.
  * **StandPrep**:  Initialization behavior for entering Stand.

Below is the behavior transition diagram:

[[File:behavior_transition_diagram.jpg]]

###### Stand

Stand is a statically stable stand, and the robot will attempt to maintain balance in light of small pushes, inclines, or other applied forces. 

The Stand behavior is the central behavior, and all behavior transitions, except to User and Freeze, occur through Stand. To enter stand, the robot must be mostly upright with no appreciable linear or angular velocity. For simulation startup, StandPrep puts the robot into a suitable configuration.

###### Walk

Walk is a dynamic walking behavior that is robust to small ground height and slope disturbances. 

A walk command in the 'Command' message requires four steps specified in 'walk_params.step_queue' with the following:

 * step_index: Which step in the Walk this step data is for.
 * foot_index: Which foot (0 for left, 1 for right). Will switch to Stand mode if two consecutive steps specify the same foot.
 * duration: How long the step should take.
 * pose: Where to put the foot, in Atlas world frame. Only yaw is used from the orientation quaternion.

The controller requires a queue of four steps to execute a stable walk. As few as two steps may be used, but it will be less stable and may switch to a Stand behavior. The step_queue can be re-specified while the current queue is executed, but it may result in instability. The next four steps needed of a longer trajectory can be determined by observing the 'walk_feedback.next_step_index_needed' field of the 'atlas_sim_interface_state' topic.

Once a foot has been lifted, the step pose cannot be changed. The Walk behavior will do its best to follow the step data, but it may have to modify steps to fit within constraints, or maintain stability. Observing the 'walk_feedback.step_queue_saturated' in the 'atlas_sim_interface_state' can provide insight into whether a trajectory should be replanned.

###### Step

Step is a quasi-static walking behavior that will realize better foot placement accuracy than walk, but is still subject to kinematic constraints.

A step command is specified in the 'step_params.desired_step' of the 'Command' message. If the controller modifies a step to meet constraints, feedback will be provided in the 'step_feedback.desired_step_saturated' of the 'State' message.

The Step behavior has two states that are specified in 'step_feedback.status_flags' of the 'State' message. The step_data in 'desired_step' can be changed when it enters the STEP_SUBSTATE_SWAYING sub-state.

###### Manipulate

Manipulate is similar to stand, except it makes more joints available for user control. The user must set the pelvis orientation, height, and position relative to the center of the feet. The user can control the movement of the back and upper body joints. The controller will be robust to added masses likely to occur during manipulation situations.

Extreme, or quick moves can overwhelm the controller's ability to maintain stability. It is also recommended that the feet be placed with step commands into strong, and stable positions.

###### Freeze

Behaviors automatically enter the Freeze state when it is determined that the robot has entered an unrecoverable state. It prevents the controller from becoming unstable.

###### StandPrep

StandPrep is a special case behavior that assumes the robot is in a 'harnessed' state. It moves the joints into a position that is suitable for stand when gravity is turned on.

###### Foot Reference Frames
Foot points indicated by [foot_pos_est](https://bitbucket.org/osrf/drcsim/src/e7323d090b95fbadcc96c1402b57f9251adc901a/ros/atlas_msgs/msg/AtlasSimInterfaceState.msg?at=default#cl-38) are offset `(0.06 0.0 -0.085) meters (x y z)` in the foot frame for both left/right feet. This value is subject to change (though we have no plans to do so at the moment.)

##### Controller ROS API

The ROS API provides four key topics that are expected to be used in controlling the Atlas robot:

  * [`/atlas/atlas_state`](https://bitbucket.org/osrf/drcsim/src/default/ros/atlas_msgs/msg/AtlasState.msg?at=default):  This topic provides the user with the current state of all joints, IMU and force torque sensors.
  * [`/atlas/atlas_command`](https://bitbucket.org/osrf/drcsim/src/default/ros/atlas_msgs/msg/AtlasCommand.msg?at=default):  This topic provides set-points and gains for a set of low-level PID controllers that operate on a per-joint basis.  (This is a slight extension to `/atlas/joint_command` with addition of PID coefficients, see the [https://bitbucket.org/osrf/osrf-common/raw/default/ros/osrf_msgs/msg/JointCommands.msg message documentation] for the control law that is implemented).  Users are expected to write higher-level behavior as ROS nodes that command these per-joint controllers to achieve coordinate motion such as balancing and walking.
  * [`/atlas/atlas_sim_interface_command`](https://bitbucket.org/osrf/drcsim/src/default/ros/atlas_msgs/msg/AtlasSimInterfaceCommand.msg?at=default):  The AtlasSimInterface Behavior Library control command can be issued over this ROS topic.
  * [`/atlas/atlas_sim_interface_state`](https://bitbucket.org/osrf/drcsim/src/default/ros/atlas_msgs/msg/AtlasSimInterfaceState.msg?at=default):  Example high-level behavior control can be seen in [this tutorial](http://gazebosim.org/wiki/Tutorials/drcsim/2.4/keyboard_teleop), which utilizes an underlying [demo actionlib server](https://bitbucket.org/osrf/drcsim/src/default/ros/atlas_msgs/actionlib_server.cpp?at=default) that closes the loop on `/atlas/atlas_sim_interface_command` and `/atlas/atlas_sim_interface_state`.

###### Controller Blending

Parameter `k_effort` can be used to switch / blend controller torques from `AtlasCommand` and `AtlasSimInterfaceCommand`.  Please see the [Control Mode Switching Tutorial](http://gazebosim.org/wiki/Tutorials/drcsim/2.4/control_mode_switching) for more details on how to switch between servo control mode and AtlasSimInterface Behavior Library control mode.

##### Update Rates

Regarding update rates, we currently expect that:

* the simulation timestep will be 0.001s (1ms);
* the update rate for the per-joint controllers running inside Gazebo (the sink for the `/atlas/joint_commands` topic) will be 1KHz (i.e., they will update every simulation timestep); and
* users will be able to write controllers external to simulation, as ROS nodes, that interact with the per-joint controllers at 200Hz-500Hz (we will narrow this range as we can with performance data).

##### Control Strategies

Regarding control strategies:

* to implement conventional PID control, set the commanded effort to zero;
* to implement torque control, set the PID gains to zero (and presumably set the commanded effort to non-zero); and
* to mix PID control and torque control, command non-zero PID gains and non-zero effort (the resulting torques will be summed).

#### Sandia hands
Control of the Sandia hands is expected to be similar to control of Atlas.  Any expected differences will be documented here.







## Qualifications

### Extra instructions for late Qualification

'''IMPORTANT''': For teams doing qualifying runs on or after May 17th, 2013, extra steps are required to get your system configured to use the right versions of software and models (the released versions have been updated in preparation for Practice and Competition).

1. Installation: download and manually install specific versions of the code (assuming here that you're working on 64-bit Ubuntu 12.04 (Precise)):

        # Install with apt-get to resolve dependencies, then uninstall
        sudo apt-get update
        sudo apt-get install -y drcsim
        sudo apt-get remove -y drcsim gazebo osrf-common sandia-hand
        # Download specific versions
        wget http://gazebosim.org/assets/distributions/osrf-common_1.0.6-1~precise_amd64.deb
        wget http://gazebosim.org/assets/distributions/sandia-hand_5.1.13-1~precise_amd64.deb
        wget http://gazebosim.org/assets/distributions/gazebo_1.7.3-1~precise_amd64.deb
        wget http://gazebosim.org/assets/distributions/drcsim_2.5.2-1~precise_amd64.deb
        # Manually install with dpkg
        sudo dpkg -i gazebo_1.7.3-1~precise_amd64.deb
        sudo dpkg -i osrf-common_1.0.6-1~precise_amd64.deb
        sudo dpkg -i sandia-hand_5.1.13-1~precise_amd64.deb
        sudo dpkg -i drcsim_2.5.2-1~precise_amd64.deb
        # Remove any cached models
        rm -rf ~/.gazebo/models

1. Configuration: point Gazebo at the archived version of the online model database (*do this in every shell you use*):

        # Usual setup
        . /usr/share/drcsim/setup.sh
        # Use a special archive of models
        export GAZEBO_MODEL_DATABASE_URI=http://gazebosim.org/models_vrc_quals/
        

### Software Versions

**Gazebo** 1.7.3

**DRC Sim** 2.5.2

**Sandia Hands** 5.1.13

**OSRF Common** 1.0.6

CloudSim is not used for Qualification. 

### Creating a Qualification Submission

#### Step 1: Record the operator and display videos

Record the operator and display videos following the procedure detailed in the [https://www.theroboticschallenge.org/_SiteImages/Discussions/VRC%20Video%20Guide%20v3%20Good.pdf Video Guide].

#### Step 2: Start a Qualification Task

**Important:** Data is stored in `/tmp/qual_task_{n}`, where {n} is the number of the Qualification task. Old data will be overwritten. Make sure to backup your data between runs.

Launch one of the Qualification tasks using a [[DRC/UserGuide#VRC_Qualification_launch_files | ROS launch file]].

#### Step 3: Perform the Run

Using some combination of teleoperation and autonomy, achieve the task.  When you're happy with the run, move onto the next step.  The simulation will not stop automatically on task completion.

#### Step 4: Stop a Qualification Task

  1. Stop logging

    ~~~
    gzlog stop
    ~~~

    The simulation will be paused while the buffered log data is flushed and written to the log file. This can take a very long time. In our testing, it can take about as long as the time required for the simulation itself. Once the log file is finished writing, the simulation will resume.

  2. **Wait until the last line in the `state.log` file is `</gazebo_log>`**. This can be verified with:

    ~~~
    $ tail -n 1 -f /tmp/qual_task_1/state.log
    </gazebo_log>$
    ~~~

  3. Quit Simulation using ctrl-c

#### Step 5: Verify the output
Verify the existence of two files upon completion of a Qualification task.

  1. A Gazebo state log file, called `state.log` should exist in `/tmp/qual_task_{n}/`, where {n} is the number of the Qualification task.
  2. A Qualification score file, called `score.log` should exist in `/tmp/qual_task_{n}/`, where {n} is the number of the Qualification task.

#### Step 6: Validate the output

  1. Replay the Gazebo state log file. This will make sure that the data is valid.

    ~~~
    gazebo -p /tmp/qual_task_{n}/state.log
    ~~~

  2. Inspect the score log file by opening it in your favorite editor.

    ~~~
    gedit /tmp/qual_task_{n}/score.log
    ~~~

    The contents will contain a header that describes the data. Make sure the data is correct.

#### Step 7: Create a zip file for log submission

Run the `mkqual.bash` script with three command line arguments:

  1. The number of the Qualification task: 1, 2, 3 or 4
  2. The Gazebo state log file: `/tmp/qual_task_{n}/state.log`
  3. The score log file: `/tmp/qual_task_{n}/score.log`

Example:
~~~
mkqual.bash 1 /tmp/qual_task_1/state.log /tmp/qual_task_1/score.log
~~~

Note that this script may take 5 minutes / 100 MB in state.log.

A new file will be created in your current directory called `vrc_qual_{n}.zip`.

Unzipping this log file should produce the `state.log` and `score.log` files.

#### Step 8: Upload the zip log file to the VRC Portal

Log into the [http:///vrcportal.osrfoundation.org VRC Portal], and submit your log file.

Only the most recent zip file for each qualification task will be kept.

It is a good idea to download the file that was just uploaded and replay the contained log data. This will verify that the upload was successful.

#### Step 9: Upload the videos to the VRC Portal

Create a single file `vrc_video_q{n}.zip` , where `n` is the number of the Qualification task (1, 2, 3 or 4). The zip file should contain the operator and screen videos following the naming convention described in the [https://www.theroboticschallenge.org/_SiteImages/Discussions/VRC%20Video%20Guide%20v3%20Good.pdf Video Guide].

Example:
~~~
zip vrc_video_q1.zip 2013_04_30_13_31_C001_OCS_Walk_1.mp4 2013_04_30_13_31_C001_OP_Walk_1.mts
~~~

Go to the ''VRC 2013 Videos'' tab of your VRC Portal team's page, and upload your video.

Only the most recent zip video for each qualification task will be kept.


## Practice

For instructions on using your cloud-hosted constellation during Practice, see the [[CloudSim/VRCUserGuide|CloudSim VRC User Guide]].
