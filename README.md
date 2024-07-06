# Gazebo Simulation for Distributed Robots
Setup for running multiple distributed robots on the same Gazebo simulation using Multimaster-FKIE ROS 1 package

## Prerequisites
1. ROS 1 Noetic
2. The network between the server running the Gazebo simulation and the robots must be set up properly. More info: https://wiki.ros.org/ROS/NetworkSetup
3. Dockerfiles are provided if you want to use a container

## Network Configuration
Enable `ip_forward` and disable `icmp_echo_ignore_broadcasts` in the Gazebo simulation server and robot's machines
   ```bash
   sudo sh -c "echo 1 > /proc/sys/net/ipv4/ip_forward"
   sudo sh -c "echo 0 > /proc/sys/net/ipv4/icmp_echo_ignore_broadcasts"
   ```

## Model Configuration
Before we can run the simulation, we need to configure the robot’s model to publish the transformations properly. We can do that by editing the model’s  `.urdf` file to accept a parameter called `robot_name`, and integrate this parameter to prefix the odometry and base_footprint frame id. Prefix any other topics/TF frames that you need to separate between the robots

I've included an example Turtlebot3 waffle and waffle_pi model that has been modified in this repository

## Running the Simulation
### Gazebo server
1. Edit the `multimaster_gazebo.launch` file in the `gazebo_server` folder and add the hostnames of the robot's machine you want to connect to the Gazebo simulation
2. Run the launch file
   ```bash
   roslaunch multimaster_gazebo.launch
   ```
### Robot machine
1. Edit the `multimaster_robot.launch` file in the `robot_machine` folder and add the hostname of the server running the Gazebo simulation
2. (Optional) Add the other robot's machine hostnames to the ignore hosts parameter in `multimaster_robot.launch`
3. Run the launch file
   ```bash
   roslaunch multimaster_robot.launch
   ```
4. Wait until the robot machine has connected and synchronized the ROS network with the Gazebo server (there should be a log printed after roslaunch)
