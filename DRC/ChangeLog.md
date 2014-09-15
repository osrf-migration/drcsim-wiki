See also [Roadmap](https://bitbucket.org/osrf/drcsim/wiki/DRC/Roadmap).

# drcsim 4.0.x

Works with Gazebo 3.0.x.

## drcsim 4.0.0 (2014-09-03)

* Atlas V3 Behavior Controller (AtlasSimInterface)
    * AtlasSimInterface 1.1.1 is still installed as `[install prefix]/[system library path]/libAtlasSimInterface.so`.  While AtlasSimInterface 2.10.2 candidate installed as `libAtlasSimInterface2.so`.
    * Updated [AtlasV3Plugin](https://bitbucket.org/osrf/drcsim/src/1d087e37896a80b592f2431c87f21c72c658d50b/drcsim_gazebo_ros_plugins/src/AtlasV3Plugin.cpp?at=drcsim_4.0.0) to work with installed `libAtlasSimInterface2.so` (AtlasSimInterface 2.10.2) library.  DRCSim now ships with a `libAtlasSimInterface2.so` shim library.  The official BDI AtlasSimInterface 2.10.2 library is still under development. [Here are Atlas v3 model instructions to drop the official BDI proprietary AtlasSimInterface 2.10.2 binary in place once it's ready](http://gazebosim.org/tutorials?tut=drcsim_install&cat=drcsim#AtlasSimulationInterface2.10.2).
    * Skip `libAtlasSimInterface` for 32bit platforms ([issue #406](https://bitbucket.org/osrf/drcsim/issue/406/do-not-install-libatlassiminterface-in)).

* Model Updates:
    * Gazebo World Models: export stand along SDF versions of Atlas worlds and models ([pull request #408](https://bitbucket.org/osrf/drcsim/pull-request/408/add-standalone-versions-of-models/activity), [pull request #405](https://bitbucket.org/osrf/drcsim/issue/405/cant-insert-some-models-atlas-from-the)).
    * Sandia hand updates
        * Fix Sandia hand camera rotations (gazebo bug fix. [issue #401](https://bitbucket.org/osrf/drcsim/issue/401/sandra-hand-cameras-wrong-orientation), [pull request #916](https://bitbucket.org/osrf/gazebo/pull-request/916/fix-for-camera-rotation-bug-issue-920/diff), [pull request #960](https://bitbucket.org/osrf/gazebo/pull-request/960/add-test-from-camera_rotation_fix-branch/diff), [pull request #961](https://bitbucket.org/osrf/gazebo/pull-request/961)).
        * Issue #408 The sandia hand plugin required both a left and right hand model. Updated the plugin to take a side parameter like the irobot hand plugin.  [Pull request #450](https://bitbucket.org/osrf/drcsim/pull-request/450).
        * Update Sandia hand inertia for trimesh version urdf ([Sandia hand pull request #41](https://bitbucket.org/osrf/sandia-hand/pull-request/41/address-drcsim-issue-400-https/diff)).
    * Update iRobot hand model and add a simulated gazebo plugin controller.  Fix iRobot hand orientation, publish joint transforms for rviz ([issue #398](https://bitbucket.org/osrf/drcsim/issue/398/update_irobot_hand-left-hand-rotate-180deg), [pull request #431](https://bitbucket.org/osrf/drcsim/pull-request/431/make-irobot-hand-publish-joint-transforms/diff)).
    * MultiSense SL Head Sensor Model
        * Update Multisense inertias ([issue #386](https://bitbucket.org/osrf/drcsim/issue/386/multisense-sl-urdf-compatibility) and [issue #397](https://bitbucket.org/osrf/drcsim/issue/397/clarify-which-multisense-inertias-should)).
    * Atlas V3 simple collision shapes created [pull request #449](https://bitbucket.org/osrf/drcsim/pull-request/449/simple-shapes-for-atlas-v3)

* Debian Dependencies:
    * Remove unused [pr2_mechanism dependencies](https://bitbucket.org/osrf/drcsim/pull-request/455/pr2_mechanism-is-not-a-package-this-breaks) and [pr2 package dependencies](https://bitbucket.org/osrf/drcsim/pull-request/456/remove-deprecated-files-and-code-which).

* DRCSim Tutorials:
    * [Tutorials migrated to new location](http://gazebosim.org/tutorials?cat=drcsim).

* Debian distributions moved to [new server](http://old.gazebosim.org/assets/distributions/).

# drcsim 3.2.x

Works with

  * gazebo-2.0.0+
  * sdformat-1.4.9+
  * sandia-hand 5.2.0+
  * osrf-common-1.1.0+

## drcsim 3.2.0 (2014-04-17)
* fix [issue #369](https://bitbucket.org/osrf/drcsim/issue/369/vrcscoringplugin-cant-find-atlas-with-new), [testing deferred load for scoring plugin](https://bitbucket.org/osrf/drcsim/pull-request/437/testing-deferred-load-for-scoring-plugin).
* fix [issue #385](https://bitbucket.org/osrf/drcsim/issue/385/teleop-walk-mode-based-on), [add fake behavior support](https://bitbucket.org/osrf/drcsim/pull-request/417/add-fake-behavior-support-385).
* fix [issue #350](https://bitbucket.org/osrf/drcsim/issue/350/behavior-enums-for) by [matching up behavior enums in ROS msg files and `AtlasSimInterface` headers](https://bitbucket.org/osrf/drcsim/pull-request/421/match-up-behavior-enums-350/diff)
* fix [issue #398](https://bitbucket.org/osrf/drcsim/issue/398/update_irobot_hand-left-hand-rotate-180deg), [flip irobot hand orientation](https://bitbucket.org/osrf/drcsim/commits/99b1b6200b7f87d078b80ebe48a3cf12dea696b5)
* address [issue #373](https://bitbucket.org/osrf/drcsim/issue/373/provide-detailed-release-notes), [add standalone versions of models](https://bitbucket.org/osrf/drcsim/pull-request/408/add-standalone-versions-of-models)
    * [modify xslt to replace all instances of `atlas_description` with atlas (or `atlas_v3`) when generating standalone gazebo models. Install standalone models in `/share/drcsim_gazebo_standalone_models/`, as opposed to being nested inside `atlas_description`.](https://bitbucket.org/osrf/drcsim/commits/5dc8baa9662c2d8edf61048a3973d7da007a879a)
* fix [issue #272](https://bitbucket.org/osrf/drcsim/issue/272/setting-sensor-rates), [change multisense_sl camera update rate topic name from /multisense_sl/fps to /multisense_sl/set_fps](https://bitbucket.org/osrf/drcsim/pull-request/436/changing-multisense_sl-camera-update-rate/diff)
* fix [issue #139](https://bitbucket.org/osrf/drcsim/issue/139/irobot-hand-fingers-dont-have-joint) and [issue #398](https://bitbucket.org/osrf/drcsim/issue/398/update_irobot_hand-left-hand-rotate-180deg), [make irobot hand publish joint transforms](https://bitbucket.org/osrf/drcsim/pull-request/431/make-irobot-hand-publish-joint-transforms/diff).
* [fix drc practice task 8 fire hose thread connect](https://bitbucket.org/osrf/drcsim/pull-request/428/fix-drc-practice-task-8-fire-hose/diff)
* [update to raw, meshes, and bdi_parser](https://bitbucket.org/osrf/drcsim/pull-request/434/update-to-raw-meshes-and-bdi_parser/diff).
* [suppport for the Polaris XP900 vehicle](https://bitbucket.org/osrf/drcsim/pull-request/416/suppport-for-the-polaris-xp900-vehicle/diff)


# drcsim 3.1.x

Works with

  * gazebo-2.0.0+
  * sdformat-1.4.9+
  * sandia-hand 5.2.0+
  * osrf-common-1.1.0+

## drcsim 3.1.1
* [fix setup.sh to source ROS setup.bash](https://bitbucket.org/osrf/drcsim/pull-request/418/backport-setupsh-cleanup-to-drcsim_31)
* Change in dependencies. Use the ros-$distro-gazebo-pkgs under the name of ros-$distro-gazebo-*-current. Same source code.

## drcsim 3.1.0

* Switch dependencies from ROS Fuerte to ROS Groovy.
* [Catkinize ros packages](https://bitbucket.org/osrf/drcsim/issue/143/catkin-ize-ros-packages-in-drcsim-and).  New drcsim package structure after catkinization:
    * Package Breakdown
        * irobot_hand_description:  URDF description of the iRobot Hand model.
        * multisense_sl_description:  URDF description of the MultiSense SL sensor head.
        * atlas_description:  URDF description of the Atlas robot.
        * atlas_msgs:  Contains `msg`, `srv`, `action` for Atlas and DRCSim.
        * drcsim_gazebo:  Previously `atlas_utils`.  Contains launch files and run-time configuration files.
        * drcsim_model_resources:  Contains Gazebo model resources (media, models, world files).
        * drcsim_gazebo_plugins:  Contains Gazebo (non-ROS) plugins previously located in `atlas_msgs`.
        * drcsim_gazebo_ros_plugins:  Contains Gazebo ROS plugins previously located in `atlas_msgs`.   As of drcsim-3.1.0, `drcsim_gazebo_ros_plugins` depends directly on [`gazebo_ros_pkgs`](https://github.com/ros-simulation/gazebo_ros_pkgs) and copies of standard Gazebo-ROS plugins have been removed form drcsim.  `gazebo_ros_pkgs` has been released as a standard ROS package in Hydro, but not in Groovy.  In Groovy, `ros-groovy-gazebo-ros-pkgs` are custom built and hosted by OSRF apt repo.
        * drcsim_tutorials:  Miscellaneous tutorials for DRCSim.  This package contains just the source files, not compiled and not installed to system target.
        * tools:  Compile time code checking tools.  Used at build time, these files are not installed to system target.
    * Major Changes:
        * Xacro build-time dependency have been removed.  Atlas robot xacros are no longer expanded during the build process.  No more [dynamic Gazebo robot model generation](https://bitbucket.org/osrf/drcsim/src/87c1930181b966c67f52aa260c1c918da66dbe5f/ros/atlas_description/robots/CMakeLists.txt?at=default#cl-19) at build time.  Xacro is invoked during launch to insert the expanded URDF onto the ROS parameter server under `robot_description`.
        * Atlas robot models are no longer included in the Gazebo world files.  It is now spawned from ROS parameter `robot_description` in [`VRCPlugin::UpdateStates`](https://bitbucket.org/osrf/drcsim/src/ba6af7779c57f3389eae6d21efd97d460ec97384/drcsim_gazebo_ros_plugins/src/VRCPlugin.cpp?at=catkin#cl-1044).  Corresponding ROS Parameter `robot_initial_pose` is used to [position the robot](https://bitbucket.org/osrf/drcsim/src/ba6af7779c57f3389eae6d21efd97d460ec97384/drcsim_gazebo_ros_plugins/src/VRCPlugin.cpp?at=catkin#cl-1108) in the world.
        * `VRCScroingPlugin` is not working due to changes to the robot spawning process.
        * World files in `vrc_arenas` have been merged into [`drcsim_model_resources/worlds`](https://bitbucket.org/osrf/drcsim/src/ba6af7779c57f3389eae6d21efd97d460ec97384/drcsim_model_resources/worlds?at=catkin).
        * Launch files in `vrc_arenas` have been merged into [`drcsim_gazebo/launch`](https://bitbucket.org/osrf/drcsim/src/ba6af7779c57f3389eae6d21efd97d460ec97384/drcsim_gazebo/launch?at=catkin).
        * DRCSim install targets are no longer versioned, with the exception of [`AtlasSimInterface 1.1.1 library binary`](https://bitbucket.org/osrf/drcsim/src/ba6af7779c57f3389eae6d21efd97d460ec97384/drcsim_model_resources/AtlasSimInterface_1.1.1?at=catkin).

# drcsim 3.0.x

 * Runs with Gazebo 1.9.x.

## drcsim 3.0.0 (2013-09-14)

* [Add tutorials for hardware / simulation bridging](https://bitbucket.org/osrf/drcsim/pull-request/364/add-tutorials-for-hardware-simulation/diff), [See issue #337](https://bitbucket.org/osrf/drcsim/issue/337/update-atlassiminterface-as-bdi-evolves).
* Add DRC practice tasks / worlds.  E.g. [Pull request #362](https://bitbucket.org/osrf/drcsim/pull-request/362/added-drc-practice-task-3-world).  [Pull request #365](https://bitbucket.org/osrf/drcsim/pull-request/365/first-pass-at-drc-practice-driving-task).
* Up-to-date Atlas meshes, kinematics and inertia [drcsim pull request #373](https://bitbucket.org/osrf/drcsim/pull-request/373/copy-new-atlas_v3-model-from-catkinized/diff).

# drcsim 2.7.x

Compatible with Gazebo 1.9.x and SDFormat 1.4.x

## drcsim 2.7.0 (2013-07-24)
* Added VRC finals worlds.
* Updated wrench message per [change in Gazebo](https://bitbucket.org/osrf/drcsim/pull-request/358/use-gazebos-new-wrench-msg-format/diff).

# drcsim 2.6.x

Compatible with Gazebo 1.8.x.

## drcsim 2.6.6 (2013-06-13)
* Fix start up race condition per [issue #326](https://bitbucket.org/osrf/drcsim/issue/326/multisense-camera-images-do-not-always) via [pull request #353](https://bitbucket.org/osrf/drcsim/pull-request/353/check-camera-util-is-initialized-before/diff).

## drcsim 2.6.5 (2013-06-07)
* Fix ATLAS head friction[https://bitbucket.org/osrf/drcsim/pull-request/346]
* Fix race condition in /atlas/set_pose[https://bitbucket.org/osrf/drcsim/pull-request/345]
* added alternate world start locations[https://bitbucket.org/osrf/drcsim/pull-request/352]

## drcsim 2.6.4 (2013-06-04)
* Fix forward-neutral-reverse switch visual[https://bitbucket.org/osrf/drcsim/pull-request/341]
* Added valgrind scripts[https://bitbucket.org/osrf/drcsim/pull-request/338][https://bitbucket.org/osrf/drcsim/pull-request/340]
* Save data from gzlog tests about memory and timing in ROS_TEST_RESULTS[https://bitbucket.org/osrf/drcsim/pull-request/337]
* The torque limits for both left and right uhz joint should be +/-110Nm[https://bitbucket.org/osrf/drcsim/pull-request/335]
* Tests to check for cheating[https://bitbucket.org/osrf/drcsim/pull-request/339]
* Make gate numbers 1-based when printing message in score.log and in /vrc_score[https://bitbucket.org/osrf/drcsim/pull-request/343]

## drcsim 2.6.3 (2013-05-28)
* Added more scoring tests[https://bitbucket.org/osrf/drcsim/pull-request/322][https://bitbucket.org/osrf/drcsim/pull-request/323][https://bitbucket.org/osrf/drcsim/pull-request/324][https://bitbucket.org/osrf/drcsim/pull-request/330/][https://bitbucket.org/osrf/drcsim/pull-request/331/][https://bitbucket.org/osrf/drcsim/pull-request/333/]
* Increased Atlas knee joint torque limit to 400Nm[https://bitbucket.org/osrf/drcsim/pull-request/325]
* Output keyboard teleop instructions to screen[https://bitbucket.org/osrf/drcsim/pull-request/327]
* Increase upper limit of ankle joint from 0.698 to 0.9 radians[https://bitbucket.org/osrf/drcsim/pull-request/328]
* Added launch file and worlds for CPU based lasers[https://bitbucket.org/osrf/drcsim/pull-request/317]
* Modify ContactModelPlugin (used by SandiaHandPlugin's tactile sensors) to use custom contact publishers[https://bitbucket.org/osrf/drcsim/pull-request/326]
* Increased friction in Sandia hand model[https://bitbucket.org/osrf/sandia-hand/pull-request/30]
* Performance improvements[https://bitbucket.org/osrf/drcsim/pull-request/329/]
* Fixed bug in camera ROS subscription logic[https://bitbucket.org/osrf/drcsim/pull-request/332/]
* Fixed reflection errors in collision geometry for left Sandia hand[https://bitbucket.org/osrf/sandia-hand/pull-request/32]

## drcsim 2.6.2 (2013-05-23)
* Use ROS param to specify logdir [pull request #321](https://bitbucket.org/osrf/drcsim/pull-request/321/scoring-testing-allow-rosparam-as-logdir).
* Quite down output [pull request #314](https://bitbucket.org/osrf/drcsim/pull-request/314/quiet-down-console-output).
* Make wall time the elapsed time from start of run [pull request #310](https://bitbucket.org/osrf/drcsim/pull-request/310/make-wall_time-the-elapsed-time-from-the).
* Fix material reference problems [pull request #315](https://bitbucket.org/osrf/drcsim/pull-request/315/fix-material-reference-problem-issue-294).
* Don't count falls after task completion [pull request #313](https://bitbucket.org/osrf/drcsim/pull-request/313/dont-count-falls-after-task-completion).
* Drive teleop tutorial [pull request #311](https://bitbucket.org/osrf/drcsim/pull-request/311/add-slider-teleop-for-drc_vehicle-using).
* Remove Atlas feet auto-disable [pull request #309](https://bitbucket.org/osrf/drcsim/pull-request/309/remove-auto-disable-for-atlas).

## drcsim 2.6.1 (2013-05-18)
* [Fix to `mud_atlas` model loading](https://bitbucket.org/osrf/drcsim/pull-request/306/fix-a-texture-and-visual-problem/diff)
* [Fix to hand camera tests](https://bitbucket.org/osrf/drcsim/pull-request/304/fix-hz-targets-in-sandia-hands-camera/diff)

## drcsim 2.6.0 (2013-05-17)
* Development aids in the [ROS API](http://gazebosim.org/wiki/DRC/UserGuide#ROS_APIs) are disabled by default.  Use [environment variables](http://gazebosim.org/wiki/DRC/UserGuide#Environment_variables) to enable them.
* BDI Dynamic Behavior Library - AtlasSimInterface 1.1.0 ROS API data structure changes expected.
    * Differences in ROS API from AtlasSimInterface 1.0.8 released in drcsim 2.4.x to AtlasSimInterface 1.1.0 in  drcsim 2.6.x are listed below:
        * [`AtlasBehaviorFeedback.msg`](https://bitbucket.org/osrf/drcsim/src/a716c12de7dbc9b63036be5f489c67b25db4278f/ros/atlas_msgs/msg/AtlasBehaviorFeedback.msg?at=drcsim_2.5): `stand_feedback`, `step_feedback`, `walk_feedback` and `manipulate_feedback` have been moved into [`AtlasSimInterfaceState.msg`](https://bitbucket.org/osrf/drcsim/src/364ac70f680b/ros/atlas_msgs/msg/AtlasSimInterfaceState.msg?at=AtlasSimInterface_1.0.9_integration).
        * [`AtlasBehaviorStandParams.msg`](https://bitbucket.org/osrf/drcsim/src/364ac70f680b/ros/atlas_msgs/msg/AtlasBehaviorStandParams.msg?at=AtlasSimInterface_1.0.9_integration):  downgraded to just a placeholder for now, more to come.
        * [`AtlasBehaviorWalkFeedback.msg`](https://bitbucket.org/osrf/drcsim/src/364ac70f680b/ros/atlas_msgs/msg/AtlasBehaviorWalkFeedback.msg?at=AtlasSimInterface_1.0.9_integration): `step_data` renamed to `step_queue_saturated`.
        * [`AtlasBehaviorWalkParams.msg`](https://bitbucket.org/osrf/drcsim/src/364ac70f680b/ros/atlas_msgs/msg/AtlasBehaviorWalkParams.msg?at=AtlasSimInterface_1.0.9_integration): `step_data` renamed to `step_queue`.
        * Supported behaviors: `WALK` and `STEP` will be partially supported. In [`AtlasBehaviorStepData.msg`](https://bitbucket.org/osrf/drcsim/src/364ac70f680b/ros/atlas_msgs/msg/AtlasBehaviorStepData.msg?at=AtlasSimInterface_1.0.9_integration), `z-value`(foot step height) and orientation (ground normal, foot yaw) in [`pose`](https://bitbucket.org/osrf/drcsim/src/364ac70f680b/ros/atlas_msgs/msg/AtlasBehaviorStepData.msg?at=AtlasSimInterface_1.0.9_integration#cl-8), [`swing_height`](https://bitbucket.org/osrf/drcsim/src/364ac70f680b/ros/atlas_msgs/msg/AtlasBehaviorStepData.msg?at=AtlasSimInterface_1.0.9_integration#cl-9) are not used and support will be added in later releases.
    * New features in AtlasSimInterface 1.1.0
        * `ManipulateStand` mode is now supported.
        * `Step` mode is now partially supported (`swing_height, step height and ground normal are not functional yet).
* MultiSense SL Model:
  * Camera frame rates adjustable between 1 to 30Hz (previously stated 1 to 60Hz).  Per testing on SoftLayer machines, we were unable to generate much faster than 37Hz at 800X800 pixels.
* Sandia Hand Model:
  * Add Sandia hand tactile sensors.
  * Sandia hand damping defaults to 1.0, adjustable via service call ([see ticket](https://bitbucket.org/osrf/sandia-hand/issue/3/damping-extremely-large)).
  * Sandia hand camera frame rates reduced from 60Hz to 30Hz, not adjustable for VRC.
* Mud model
* Switch hand IMU to use ImuSensors, add noise model to hand IMU outputs, see [ticket](https://bitbucket.org/osrf/sandia-hand/issue/5/add-noise-to-hand-imus).
* DRC Vehicle updates
 * Remove side handrails
 * Possibly enlarge cabin (e.g., raise roll cage).
* GPU collision detection for laser scanner.
* Added event scoring module (see [VRCScore.msg](https://bitbucket.org/osrf/drcsim/src/a0a9799d787df62888fecd85d84dae3bf5b22411/ros/atlas_msgs/msg/VRCScore.msg?at=default)).
* Updated fire hose model (thinner with ergonomic grip).
<gallery>
File:vrc3_firehose_drcsim_2_6.png|updated VRC3 environment
</gallery>

# drcsim 2.5.x

## drcsim 2.5.2 (2013-04-22):
* [Fixed race condition on startup with behavior library](https://bitbucket.org/osrf/drcsim/pull-request/224/fix-start-race-condition-if-world-starts)

## drcsim 2.5.0 (2013-04-19):
* Set default iterations to 50 and SOR to 1.4 [https://bitbucket.org/osrf/drcsim/pull-request/202/make-default-iterations-50-sor-14-and-copy/diff]
* Added support for Gazebo state and score logging [https://bitbucket.org/osrf/drcsim/pull-request/213/added-qual-zip-script/diff]
* Added script to generated Qual submissions [https://bitbucket.org/osrf/drcsim/pull-request/213/added-qual-zip-script/diff]
* Added mud plugin [https://bitbucket.org/osrf/drcsim/pull-request/209/added-a-mud-model-based-on-the-gazebo/diff]
* Integration of Atlas Teleop tools [https://bitbucket.org/osrf/drcsim/pull-request/211/adding-atlas-teleop-tools/diff]
* Atlas starts in Stand Mode [https://bitbucket.org/osrf/drcsim/pull-request/218/change-qual-1-3-4-to-start-up-in-bdi-stand]
* Reduce spacing between boxes in `qual_task_1` world.  See [ticket](https://bitbucket.org/osrf/drcsim/issue/200/boxes-are-too-far-apart-in)

# drcsim 2.4.x:
Compatible with Gazebo 1.6.x

## drcsim 2.4.0 (2013-04-15):
* [Integrated AtlasBehaviorLibrary 1.0.8](https://bitbucket.org/osrf/drcsim/pull-request/193):
 * runs with default solver parameters
 * includes multiple behaviors
 * exposes new [ROS API for AtlasSimInterface Behavior Library](http://gazebosim.org/wiki/DRC/UserGuide#Boston_Dynamics_AtlasSimInterface_ROS_API_.28DRCSim_2.4_and_Later.29).
   **Note:**  This is a limited functionality release, only partial `STAND_PREP`, `STAND` and `WALK` functionalities are working as of this release.
     Most of the parameters in [`AtlasSimInterfaceCommand.msg`](https://bitbucket.org/osrf/drcsim/src/14e4dbf73261a4537b8864c9b64f6db31c06b974/ros/atlas_msgs/msg/AtlasSimInterfaceCommand.msg?at=AtlasSimInterface_1.0.9_integration) and [`AtlasSimInterfaceState.msg`](https://bitbucket.org/osrf/drcsim/src/14e4dbf73261/ros/atlas_msgs/msg/AtlasSimInterfaceState.msg?at=AtlasSimInterface_1.0.9_integration) are not yet supported.
     In particular, not much beyond walking on flat ground (as demonstrated in [this tutorial](http://gazebosim.org/wiki/Tutorials/drcsim/2.4/keyboard_teleop)) is working as of this release.  For upcoming features, see [RoadMap](http://gazebosim.org/wiki/DRC/Roadmap).
* MultiSense-SL camera horizontal and vertical field of view [switched to 80degX80deg @ 800X800pixels](https://bitbucket.org/osrf/drcsim/pull-request/188)
* [Updated friction coefficients](https://bitbucket.org/osrf/drcsim/pull-request/199) for Atlas links.
* [Minor fixes](https://bitbucket.org/osrf/drcsim/pull-request/191) to Atlas effort limits and link inertias.

# drcsim 2.3.x:
Compatible with Gazebo 1.6.x

## drcsim 2.3.1 (2013-04-09):
* Added `stereo_image_proc` for Sandia hand cameras, which had been [missing](https://bitbucket.org/osrf/drcsim/issue/178).
* [Fixed bug in use of BDI behavior library](https://bitbucket.org/osrf/drcsim/pull-request/183).

## drcsim 2.3.0 (2013-04-05):
* Added [Sandia hand cameras](https://bitbucket.org/osrf/sandia-hand/pull-request/19/fix-camera-topics-for-drcsim-without/diff).
* Added ROSAPI tests to automatically check available ROS topics offered by the Atlas robot.
* Added ROS topics `/atlas/atlas_state` and `/atlas/atlas_command` for control over UDP.  To prevent fragmentation, each of these messages are designed to be <1500 Bytes.
* Added `gazebo_ros_force` plugin development aide.
* Added [camera sensor noise](https://bitbucket.org/osrf/drcsim/src/5756680c9e94/ros/multisense_sl_description/urdf/multisense_sl.urdf?at=default#cl-206).
* Added IMU noise for [torso imu](https://bitbucket.org/osrf/drcsim/src/5756680c9e9454a4a79d48dc344283d61ccf4f54/ros/atlas_description/urdf/atlas.gazebo?at=default#cl-42) and for [head imu](https://bitbucket.org/osrf/drcsim/src/5756680c9e94/ros/multisense_sl_description/urdf/multisense_sl.urdf?at=default#cl-367)
* Added [LIDAR sensor noise](https://bitbucket.org/osrf/drcsim/src/5756680c9e94/ros/multisense_sl_description/urdf/multisense_sl.urdf?at=default#cl-153).
* Atlas [inertia tweak](https://bitbucket.org/osrf/drcsim/pull-request/157/inertia-updates) to help solver convergence.
* Fix atlas force torque sensor to be in the right frame (see [pull request 162](https://bitbucket.org/osrf/drcsim/pull-request/162/switch-force-torque-sensors-to-use-l_hand), which resolved [issue 155](https://bitbucket.org/osrf/drcsim/issue/155/force-torque-sensor-issues)).
* Updated to use [pub_queue](https://bitbucket.org/osrf/drcsim/pull-request/153/switch-all-modelplugin-and-systemplugin).
* [kryptonite patch](https://bitbucket.org/osrf/drcsim/pull-request/167/changed-gate-textures).
* [fix camera_info publication](https://bitbucket.org/osrf/drcsim/issue/163/ros-camera-plugin-not-publishing).
* [fix imu frame_id](https://bitbucket.org/osrf/drcsim/issue/152/drcsim-22-imu-issues).
* [changed contact sensor topics to use `geometry_msgs/WrenchStamped`](https://bitbucket.org/osrf/drcsim/issue/153/foot-contact-ros-topic-published-values).
* Added texture to the fire hose, added foreground objects to VRC task 2.


# drcsim 2.2.x:
Compatible with Gazebo 1.5.x

## drcsim 2.2.0 (2013-03-11):
* '''Binary packages are 64-bit only.'''  This limitation comes from inclusion of the Atlas behavior library, which is currently available only as a 64-bit shared object.
* VRC Qualification arenas.
* Sandia hand updates
 * Updated inertia properties
* Preliminary behavior library and accompanying ROS API for higher-level control of Atlas (e.g., balancing, walking).
 * Basic standing / walking demo with BDI's closed source behavior controller.
* DRC Vehicle simulation updates.
 * Physically steerable, drive-able vehicle.
* MultiSense SL sensor head updates.
 * Update install of ros `manifest.xml` and gazebo `model.config` files.
 * Update head imu location.
 * Image generation default changed to 1MP (1536 X 816 pixels) @ 30FPS per [documentation](http://www.theroboticschallenge.org/local/documents/MultiSense_SL.pdf).
 * Improved performance with threaded sensor generation.
* Release for Ubuntu Quantal with Groovy support.
* Ability to reset internal integral terms.

# drcsim 2.1.x

Compatible with Gazebo 1.4.x

## drcsim 2.1.0 (2013-02-28)

* Add VRC Qualification worlds and launch files.

# drcsim 2.0.x

Compatible with Gazebo 1.4.x

## drcsim 2.0.1 (2013-02-01)

* Tweak example joint commands publisher ([pr#110](https://bitbucket.org/osrf/drcsim/pull-request/110/include-tcpnodelay-in-jointstates))
* Improve behavior when entering and exiting the vehicle through magic cheats ([pr#112](https://bitbucket.org/osrf/drcsim/pull-request/112/add-pause-and-unpause-reorganize-order-of))

## drcsim 2.0.0 (2013-02-01)

* [[DRC/UserGuide | Preliminary ROS API for interfacing with simulation is defined.]]
  * ROS topics updated, name spaced by subsystems, `/atlas/`, `/multisense_sl/`, `/sandia_hands/`.
  * Split out [sandia hands package](https://bitbucket.org/osrf/sandia-hand).
  * New [controller joint commmands message](https://bitbucket.org/osrf/osrf-common/raw/default/ros/osrf_msgs/msg/JointCommands.msg).
* Models files generated by [xacro](http://ros.org/wiki/xacro) at compile time.
* Introduce Polaris Ranger EV model.
* Added simple collision geometries for Atlas, Sandia hand model and Polaris Ranger EV.
* Turned off usage of [gazebo_ros_controller_manager plugin](https://bitbucket.org/osrf/drcsim/src/45a23d87af80af8bbc467a58382dba903f8572d7/ros/atlas_msgs/gazebo_ros_controller_manager.h?at=default) in default launch files.
* Updated/rearranged cmake install target directory structures.
* Switch to using cmake `ExternalProject_Add` for generating ros messages, now we can also generate ROS service messages too.
* (Developers) Infer `ROS_DISTRO` from environment setting at compile time.
* Style fixes.
* Created Sandia hands controller plugin.
* Switched `r_arm_usy` direction to match hardware.
* Added ROS topic hz rate tests for drcsim package.
* Synchronized MultiSense SL cameras for better stereo output.

# drcsim 1.3.x

Compatible with Gazebo 1.3.x.

## drcsim 1.3.1 (2013-01-02)
* No code changes.  Released only to force a rebuild of the binary .deb packages against the latest ROS .deb packages.  This rebuild fixes a mysterious segfault that was introduced by a newly released ROS package (not sure which one).

## drcsim 1.3.0 (2012-12-21)
* Added VRCPlugin, adding some default **cheat** behaviors for VRC simulation.  Also updated DRC vehicle plugin, exposing ROS topics as well as mechanical control of the vehicle.  Please consult the [tutorials](http://gazebosim.org/wiki/Tutorials/drcsim/) and [headers for documentation](https://bitbucket.org/osrf/drcsim/src/6a1c171b7329/plugins/ros/VRCPlugin.hh?at=default).
* DRC robot is now named Atlas.
* Updates to MultiSense SL LIDAR parameters ([issue #65](https://bitbucket.org/osrf/drcsim/issue/65/lidar-params-on-sensor-head)).
* Fix Atlas IMU offset per [issue #67](https://bitbucket.org/osrf/drcsim/issue/67/incorrect-offset-for-imu).

# drcsim 1.2.x
Compatible with Gazebo 1.3.x.

## drcsim 1.2.0 (2012-12-17)
* Initial draft of Atlas Robot head sensor suite made from simplified CAD model of [MultiSense SL by Carnegie Robotics](http://theroboticschallenge.org/documents/MultiSense_SL.pdf).  This first draft of the MultiSense SL sensor model contains several assumptions detailed below:
  * The IMU in the sensor head is not yet modeled.
  * The LED lights in the sensor head are not yet modeled.
  * The stereo generation is done using [stereo_image_proc](http://ros.org/wiki/stereo_image_proc) at a slower update rate (as opposed to onboard FPGA).
  * The LIDAR scanner range and angular resolution [needs to be updated](https://bitbucket.org/osrf/drcsim/issue/65/lidar-params-on-sensor-head).
  * The LIDAR spindle speed is not limited per spec and [needs to be updated](https://bitbucket.org/osrf/drcsim/issue/65/lidar-params-on-sensor-head).
  * Mass, inertial and dynamics parameters of the head sensor unit are approximate and differs from actual sensor head.
* Various patch fixes
  * Atlas robot mass now conforms to [initial mass estimations](https://bitbucket.org/osrf/drcsim/src/eb4c25838c45075bdde52c5dad60bf35c4b7d8a2/ros/drc_robot_utils/raw/drc_skeleton.cfg?at=default) without tweaks.
  * Various basic gain setting updates.  Stable open loop standing with joint position controllers.

# drcsim 1.1.x
Compatible with Gazebo 1.2.x.

## drcsim 1.1.0 (2012-11-20)
* Support running a subset of the [http://www.ros.org/wiki/robot_mechanism_controllers ROS robot_mechanism_controllers] on the entire DRC robot model (including legs).
 * Using [joint trajectory controller](http://ros.org/wiki/robot_mechanism_controllers/JointTrajectoryActionController) for the default robot launch file.
 * Added several different controller configurations in [drc robot model directory](https://bitbucket.org/osrf/drcsim/src/d8a165a341378e3869aa3976189fce09d12bbc48/models/drc_robot/ros?at=default)
 * Controllers managed (loaded, unloaded, started, stopped, commanded) in the usual way, via ROS topics.
 * Balancing and walking should be possible, though perhaps not convenient, to implement.
* Initial model of hose and coupling for use in the hose connection task.
* ROS topic `reset_world` renamed to `reset_models` [issue #32](https://bitbucket.org/osrf/drcsim/issue/32/reset_world-ros-service-should-be-renamed)
* DRCRobotPlugin modes are [nominal, no_gravity, pinned, feet].
* gazebo includes:  `physics.h` --> `physics.hh`.
* Various DRC Robot model fixes.
  * ubx upper limit
  * usy joint axis fix
  * mwx offset fix

# drcsim 1.0.x
Compatible with Gazebo 1.2.x.

## drcsim 1.0.3 (2012-11-07)
* Enabling access to online model database [https://bitbucket.org/osrf/drcsim/pull-request/23/ Details].
* Made a variety of fixes to the DRC robot model, including meshes and link names.  Added the ability to unpin the hip from the world. [https://bitbucket.org/osrf/drcsim/pull-request/24/ Details].

## drcsim 1.0.2
* Updated destructor to match changes in Gazebo. [https://bitbucket.org/osrf/drcsim/pull-request/22/ Details]

## drcsim 1.0.1
* Removed warning message. [https://bitbucket.org/osrf/drcsim/pull-request/20/ Details]

## drcsim 1.0.0
* First release. This package contains models, worlds, plugins, and ROS code (plugins, launch files) to support initial development and testing in simulation for the DRC.  This version requires gazebo 1.2.x.