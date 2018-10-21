# CarND-Path-Planning-Project
Self-Driving Car Engineer Nanodegree Program

# [Rubic](https://review.udacity.com/#!/rubrics/1020/view) Points Meet

## Compilation
- mkdir build
- cd build
- cmake ..
- make

For using splines instead of polynomials, I use a single header file spline.h from [Cubic Spline interpolation implementation](http://kluge.in-chemnitz.de/opensource/spline/). All the code compiles correctly. 

## Valid Trajectories
All requirements are met.

## Reflection
The main algorithm starts from line 239 to line 387 in main.cpp based on the provided project code. These code can be seperated into three parts, which has different function.

### Prediction
The code from line 243 to line 272 in main.cpp wants to reason about the environment by dealing with the telemetry and sensor fusion data. The code wants to make clear two facts: whether the car in front of us blocks the traffic, whether the car to the right/left of us makes a lane change not safe. The code achieves the goal by calculating the lanes other cars are and the position they will be at the end of the last plan trajectory. If the distance to our car is less than 30 meters in front or behind us, the car car is considered dangerous. 

### Behavior
The code from line 274 to line 294 in main.cpp wants to decide whether we should change lanes if a car is in front of us and decide whether we should speed up or slow down. The code increases/decreases the speed, makes a lane change if it is safe. The variable speed_diff is used to change speed when generating the trajectory, which makes the car more flexible in changing situations.

### Trajectory
The code from line 296 to line 387 in main.cpp calculates the trajectory based on the speed and lane output from the behavior, car coordinates and past path points. In line 299-345, I get the previous two points, and use them in conjunction three points at a far distance to initialize the spline calculation. In these code, the coordinates are transformed to local car coordinates to make calculation less complicated. In line 347-355, the pass trajectory points are copied to the new trajectory to ensure more continuity on the trajectory. The rest of the points are calculated by evaluating the spline and transforming the output coordinates to not local coordinates.