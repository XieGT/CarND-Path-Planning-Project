# Path Planing Project
## Goals
In this project your goal is to safely navigate around a virtual highway with other traffic that is driving +-10 MPH of the 50 MPH speed limit. You will be provided the car's localization and sensor fusion data, there is also a sparse map list of waypoints around the highway. The car should try to go as close as possible to the 50 MPH speed limit, which means passing slower traffic when possible, note that other cars will try to change lanes too. The car should avoid hitting other cars at all cost as well as driving inside of the marked road lanes at all times, unless going from one lane to another. The car should be able to make one complete loop around the 6946m highway. Since the car is trying to go 50 MPH, it should take a little over 5 minutes to complete 1 loop. Also the car should not experience total acceleration over 10 m/s^2 and jerk that is greater than 50 m/s^3.

## Basic Build Instruction
### 1. Read and define the initial car's state
#### I. define initial conditions
*  The car located in the second lane
* referance velocity ref_vel = 49.5 MPH
#### II. find car's state
* get car's position(x,y)
* based on position get car's yaw angle, and speed
* find out how many miles the car has travelled
#### III. find ahead car's state
* use sensor fusion data find the car in the front.
* find the distance between it check_car_s - car_s
* if the distance is too close, change our car's speed & mark the change_lanes = ture. 
### 2. Define left & right turn logic (line 171 - 240)
#### I. Check change lane conditions
* based on sensor fusion data(change_lanes) and map(map_waypoint) to determine if the lane change is possible
#### II. left turn
* check the condtion: not the leftmost lane & not in the middle of change lane. 
* locate the surrounding cars and find their speed to check the safety condition (left_lane_safe) 
*  change lane, and mark the waypoint.
#### III. right turn
follow the same procedure as left turn.

### 3. Path Planning (line 241 - 345)

#### I. define anchor path with 5 pts 
* use last two pts from previous path as starting points
* define three 30m evenly spaced pts in Frenet coordinates from map.
* get the anchor path with 5 defined pts using spline c++.
#### II. define real path
* find out how many pts need to be generated (50 - previous_points).
* based on anchor path find those pts. 
* adjust next car_speed. 
* push those pts in next_x_val & next_y_val.

