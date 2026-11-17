# BlueROV2 Model for Obstacle-avoidance in Gazebo Harmonic

This is an obstacle-avoidance control experiment using gazebo harmonic simulation. The simulation uses BlueROV2 with ping-sonar positioned in a forward-facing position to detect an obstacle. The environment use an 8 x 8 x 8 m underwater tank with cylinder objects placed at the U-ROV intersecting survey path. The U-ROV usses BCPP survey strategy to reach the final point.

The BlueROV2 model already include the BuoyancyPlugin, HydrodynamicsPlugin and ThrusterPlugin to better simulate the implementation.

<img width="400" height="400" alt="gz_sim" src="https://github.com/user-attachments/assets/ca449282-6850-4db1-bf4a-468157a2a734" /> 
<img width="400" height="400" alt="survey_route" src="https://github.com/user-attachments/assets/3fc55ea8-cdd9-4601-a935-6bf9d006253b" />


## Requirements

Please ensure that [Gazebo Repo](https://github.com/m4ttroy/rov_gz) and its requirements have been installed prior


## Running Gazebo Simulation + Controller

To run the gazebo, a dedicated launch file has been made at /../rov_gz/launch (see more detailed at [rov_gz README.md](https://github.com/m4ttroy/rov_gz/blob/main/README.md)) <br>
For obstacle-avoidance simulation, the launch file can be executed using

~~~bash
ros2 launch rov_sim.launch.xml
~~~

To run the controller in a seperate terminal

~~~bash
ros2 run obs_avoidance "control" 
~~~

Change the "control" to the controller matching your option
* `start` to place the U-ROV at initial point (0, 0, -5)
* `pid` to use PID controller
* `nmpc` to use N-MPC controller

N.B. for PID you can add extra argument --args -p enable_model:False to use UKF disturbance estimation or True to use known modeled disturbance


## ROS2 Topics

This are the following topics recorded for offline analysis

| Topic                | Description                     |
| -------------------- | ------------------------------- |
| `/model/rov/pose`    | ROV pose in world coordinate    |
| `/model/rov/odom`    | ROV odom in body coorinate      |
| `/model/rov/sonar`   | Ping-sonar data readings        |
| `/model/rov/imu`     | FCU IMU sensor data             |