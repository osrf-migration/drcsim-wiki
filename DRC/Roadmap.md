See also [Change Log](https://bitbucket.org/osrf/drcsim/wiki/DRC/ChangeLog).

Future changes expected:

# drcsim 4.0.x

Released with Gazebo 4.0.x
Works with Gazebo 3.0.x and 4.0.x

* Atlas V4 model
    * Matches Atlas without electric arms.
    * Arms repositioned (lower) to increase workspace.
    * Mass increase of ~15lbs
    * New actuator in knee, hip and back to address strength, backlash and compliance issues. This translates to new torque limits for the knee, hip and back actuated joints in atlas_v4 model.
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
    * Addressed issue #425 with pull request #463
 * RobotiQ S model (3 finger model)
    * Integrated with Atlas V4

## drcsim 4.1.0 (11-21-2014)

 * RobotiQ S model (3 finger model)
    * Joint coupling and API updates

## drcsim 4.2.0 (Forthcoming)

 * RobotiQ Joint coupling
 * Atlas v5 model
     * New electric arm models
 * Atlas Behavior library
    * Behaviors for Atlas v5
 * This release will contain bug fixes and updates based on issues in the DRCSim tracker.
