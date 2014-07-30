#DRCSim Release Schedule

## Motivation
This document covers the initial plan of the DRCSim team's support for ROS and Ubuntu distributions from October 2013 to the end of the DARPA Robotics Challenge.

## Ubuntu and ROS calendar 
In order to fully understand the background behind decisions on releasing and supported platforms for DRCSim, it is useful to know the expected calendar for Ubuntu and ROS distributions. 

[[Image:DRC_release_schedule.png|left|thumb|700px|Releasing calendar for ROS and Ubuntu]]

<div style="clear: both"></div>

## DRCSim calendar

Based on previous experience and all of the feedback provided by the teams in the DRC meeting (Oct 18th 2013) the DRCSim team proposes a conservative calendar with the goal of minimizing the migrations needed by the teams. No platform changes are expected for the last 8 months of the DRC, and there will be extended support even for Ubuntu or deprecated ROS distributions.

''Warning:'' The DRCSim team highly encourages users to stay on supported platforms (for both Ubuntu and ROS) if possible. Some bugs cannot be solved without an upgrade in the upstream platform, so please be careful when deciding to stay on an unsupported platform. 

### Release Milestones

* '''2014 - January:''' ''Ubuntu raring end of life''
** DRCSim keep supporting raring-hydro
** DRCSim start supporting precise-hydro
** ''Supported platforms at this moment:''
*** precise-groovy
*** precise-hydro
*** quantal-groovy
*** raring-hydro

* '''2014 - April/May:''' ''Ubuntu quantal end of life, Ubuntu Trusty 14.04 release, ROS Groovy end of life, ROS Indigo release''.
** DRCSim stop supporting quantal-groovy
** ''Supported platforms at this moment:''
*** precise-groovy
*** precise-hydro
*** raring-hydro

* '''2014 - July:''' ''Ubuntu saucy end of life''.
** DRCSim won't change any support at this time (6 moths left).
** ''Supported platforms at this moment:''
*** precise-groovy
*** precise-hydro
*** raring-hydro
