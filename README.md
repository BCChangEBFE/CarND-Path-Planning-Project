# CarND-Path-Planning-Project
Self-Driving Car Engineer Nanodegree Program.

This is my implementation for solution to Udacity course project hosted at CarND-Path-Planning-Project

## Reflection
Most of the ideas are directly from the Path Planning Walkthrough Video from the course.

### Speed 
To avoid accelerating too fast, initial reference_velocity is set at 0, while speed limit is set at 49.5mph to avoid passing speed limit. For every telemetry event that the path-planing algorithm observes, the reference_velocy may be 
 * increased by 0.224mph if safe and under speed limit
 * decreased to the higher speed of the following 2 options 
     ** speed of the leading car - 0.00001mph 
     ** current spee - 0.4mpg
 
### Path Trajectory
The next planned trajectory points to be followed are always a list of 50 points, and they consists of
 * All un-reached previous cycles planned paths as the next destination points
 * The remaining points are mapped out by a spline algorithm and the reference velocity. The input points of the spline trajectory are:
   * Previous end points as starting reference
   * 3 30meters spaced points ahead of the starting reference. Note that if a change lane manuver is in place, these 3 points could be pointing to the adjacent lane. 

### Lane Change Decision
A simple cost based algorithm is implemented. In the calculation of cost funcion, only the closest leading car and closest rear car in each lane is considered. Also the algorithm only searches for a fixed distance forward and backward while ignoreing cars that are simply too far away. For each lane a cost is calculated and the lane with smallest cost is chosen to be the next target lane. However, logic is also put in to make sure a lane change of 2 or more lane is not allowed. The cost for each lane are calculated based on the following parameters, 
 * Distance to leading car
 * Velocity of leading car
 * Number of lane changed. 
   ** i.e. cost += abs(target_lane - lane) * Constant
 * If leading car or rear is actually too close
 
The simple cost based implementation is working well and allows tuning the parameter to result in a vehicle that changes lane more aggressively. However There are many places that can potentially be improved. For example: an estimated future position of the leading and rear car should also be put into consideration; the definition of **to close** can take into consideration of ego vehicle and surrounding cars (instead of just relying on a fixed distance check).

###
An sample run of the algorithm can be found at 
https://www.youtube.com/watch?v=5pJoi-POXxw

## resources:
The basic path planning logic and code follows the implementation descripbed in:
https://www.youtube.com/watch?v=7sI3VHFPP0w

spline.h is from 
http://kluge.in-chemnitz.de/opensource/spline/spline.h

