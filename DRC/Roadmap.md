See also [Change Log](https://bitbucket.org/osrf/drcsim/wiki/DRC/ChangeLog).

Future changes expected:

# drcsim 4.0.x

Released with Gazebo 4.0.x
Works with Gazebo 3.0.x and 4.0.x

## drcsim 4.1.0 (to be released 10-17-2015)
* Atlas V4 model
    * Should match the model after Nov 15, 2014 ~ Jan 1, 2015 upgrade.
    * Arms repositioned (lower) to increase workspace.
    * Note the electric 7DOF forearms will not be ready.  The new 7DOF electric forearm is slated for another round of upgrades by BDI around Feb. 2015 and we'll have an updated model in drcsim 4.2.x.
    * Mass increase of ~15lbs
    * New actuator in knee, hip and back to address strength, backlash and compliance issues. This translates to new torque limits for the knee, hip and back actuated joints in atlas_v4 model.
 * RobotiQ S model added
    * Added new RobotiQ hand.
    * 3-Finger model.
    * Reuse controller messages from [robotiq_s_model_control](https://github.com/evenator/swri-ros-pkg/tree/master/robotiq/robotiq_s_model_control).
    * Modes of operation supported:
        * Simplified control mode.
        * Emergency auto-release.
        * Individual Control of Fingers.
* DRC Final Tasks
    * Updated works per DRC trials specifications ([link to pdf](http://archive.darpa.mil/roboticschallengetrialsarchive/sites/default/files/DRC%20Trials%20Task%20Description%20Release%2011%20DISTAR%2022197.pdf)).
    * Green, yellow, orange and red tape has been added in all of the trial worlds to delineate sub-tasks.
    * The obstacle course in Task 1 is complete. However, the robot does not start in the vehicle, as specified in the document.
    * Task 2 features new terrain segments: a level staircase formation of cinderblocks and an angled staircase formation.
    * Task 3 features 6 ladders to reflect all possible options for DRC teams: a 60 or 75 degree ladder with zero, one or two handrails.
    * Task 4 has been updated with accurate dimensions and a wider doorway.
    * The doorframes and layout in Task 5 have been updated to reflect the document. The weighted door handle requires further testing to match the trials specifications.
    * Task 6 features a wall with an triangular red, green and blue pattern to reflect the document specifications. The wall is not yet breakable, so an accurate drilling simulation will require integration of the Gazebo breakables plugin.
    * Task 7 features 3 valves attached to a solid wall. The valve dynamics require further testing and refinement to match reality.
 * Misc software updates
    * AtlasPlugin (V1)
        * merged AtlasV3Plugin
        * Cleaned up joint position and velocity filter code
