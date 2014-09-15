See also [Change Log](https://bitbucket.org/osrf/drcsim/wiki/DRC/ChangeLog).

Future changes expected:

# drcsim 4.0.x

Works with Gazebo 3.0.x.

## drcsim 4.0.0

* Updated to work with AtlasSimInterface 2.10.2 library.  DRCSim now ships with a placeholder shim library.  The official BDI library does not work yet, and is still being debugged, but [one can now drop the binary in place once it's ready](http://gazebosim.org/tutorials?tut=drcsim_install&cat=drcsim#AtlasSimulationInterface2.10.2).  

* Update iRobot hand model and add a simulated gazebo plugin controller.  Fix iRobot hand orientation, publish joint transforms for rviz ([issue #398](https://bitbucket.org/osrf/drcsim/issue/398/update_irobot_hand-left-hand-rotate-180deg), [pull request #431](https://bitbucket.org/osrf/drcsim/pull-request/431/make-irobot-hand-publish-joint-transforms/diff)).

* export stand along SDF versions of Atlas worlds and models ([pull request #408](https://bitbucket.org/osrf/drcsim/pull-request/408/add-standalone-versions-of-models/activity), [pull request #405](https://bitbucket.org/osrf/drcsim/issue/405/cant-insert-some-models-atlas-from-the)).

* Fix Sandia hand camera rotations (gazebo bug fix. [issue #401](https://bitbucket.org/osrf/drcsim/issue/401/sandra-hand-cameras-wrong-orientation), [pull request #916](https://bitbucket.org/osrf/gazebo/pull-request/916/fix-for-camera-rotation-bug-issue-920/diff), [pull request #960](https://bitbucket.org/osrf/gazebo/pull-request/960/add-test-from-camera_rotation_fix-branch/diff), [pull request #961](https://bitbucket.org/osrf/gazebo/pull-request/961)).

* Issue #408 The sandia hand plugin required both a left and right hand model. Updated the plugin to take a side parameter like the irobot hand plugin.  [Pull request #450](https://bitbucket.org/osrf/drcsim/pull-request/450).

* Skip `libAtlasSimInterface` for 32bit platforms ([issue #406](https://bitbucket.org/osrf/drcsim/issue/406/do-not-install-libatlassiminterface-in)).

* Update Multisense inertias ([issue #386](https://bitbucket.org/osrf/drcsim/issue/386/multisense-sl-urdf-compatibility) and [issue #397](https://bitbucket.org/osrf/drcsim/issue/397/clarify-which-multisense-inertias-should)).

* Update Sandia hand inertia for trimesh version urdf ([Sandia hand pull request #41](https://bitbucket.org/osrf/sandia-hand/pull-request/41/address-drcsim-issue-400-https/diff)).

* Remove unused [pr2_mechanism dependencies](https://bitbucket.org/osrf/drcsim/pull-request/455/pr2_mechanism-is-not-a-package-this-breaks) and [pr2 package dependencies](https://bitbucket.org/osrf/drcsim/pull-request/456/remove-deprecated-files-and-code-which).

* [Tutorials migrated to new location](http://gazebosim.org/tutorials?cat=drcsim).

# [drcsim 3.2.x](http://gazebosim.org/wiki/DRC/Change_log#drcsim_3.2.x)

## drcsim 3.2.1

* various bug fixes.
