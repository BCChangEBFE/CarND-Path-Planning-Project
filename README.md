# CarND-Path-Planning-Project
Self-Driving Car Engineer Nanodegree Program.

This is my implementation for solution to Udacity course project hosted at CarND-Path-Planning-Project

## Reflection
Most of the ideas are directly from the Path Planning Walkthrough Video from the course.

### Speed 
To avoid accelerating too fast, initial reference_velocity is set at 0, while speed limit is set at 49.5mph to avoid passing speed limit. For every telemetry event that the path-planing algorithm observes, the reference_velocy may be 
 - increased by 0.224mph if safe and under speed limit
 - decreased by 0.224mph if too close the the car infront and in the same lane
 
### Path Trajectory
The next planned trajectory points to be followed are always a list of 50 points, and they consists of
 * All un-reached previous cycles planned paths as the next destination points
 * The remaining points are mapped out by a spline algorithm and the reference velocity. The input points of the spline trajectory are:
  * Previous end points as starting reference
  * 3 30meters spaced points ahead of the starting reference. Note that if a change lane manuver is in place, these 3 points could be pointing to the adjacent lane. 

### Lane Change Decision
Left lane change maneuver is take if all of the below are satisfied
 * Car in front is slower too close
 * Left Lane change is if safe. Where left lane change is safe if:
  * No car in the left lane 50m infront
  * No car in the left lane 20m behind
Right lane change maneuver is take if all of the below are satisfied
 * Car in front is slower too close
 * Right lane change is safe, and left lane change is not safe. Where right lane change is safe if:
  * No car in the right lane 50m infront
  * No car in the right lane 20m behind


## resources:
The basic path planning logic and code follows the implementation descripbed in:
https://www.youtube.com/watch?v=7sI3VHFPP0w

spline.h is from 
http://kluge.in-chemnitz.de/opensource/spline/spline.h

