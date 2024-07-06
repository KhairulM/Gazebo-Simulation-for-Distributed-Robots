from osrf/ros:noetic-desktop-full-focal

# Install Turtlebot3 dependencies
run sudo apt update
run sudo apt install -y --no-install-recommends \
    wget tmux nano git \
    ros-noetic-gazebo-* ros-noetic-rgbd-launch \
    ros-noetic-joy ros-noetic-teleop-twist-joy \
    ros-noetic-teleop-twist-keyboard ros-noetic-laser-proc \
    ros-noetic-rgbd-launch ros-noetic-rosserial-arduino \
    ros-noetic-rosserial-python ros-noetic-rosserial-client \
    ros-noetic-rosserial-msgs ros-noetic-amcl ros-noetic-map-server \
    ros-noetic-move-base ros-noetic-urdf ros-noetic-xacro \
    ros-noetic-compressed-image-transport ros-noetic-rqt* ros-noetic-rviz \
    ros-noetic-gmapping ros-noetic-navigation ros-noetic-interactive-markers \
    ros-noetic-fkie-multimaster

# Install Turtlebot3
run mkdir -p /catkin_ws/src
workdir /catkin_ws/src
run git clone -b noetic-devel https://github.com/ROBOTIS-GIT/DynamixelSDK.git && \
    git clone -b noetic-devel https://github.com/ROBOTIS-GIT/turtlebot3_msgs.git && \
    git clone -b noetic-devel https://github.com/ROBOTIS-GIT/turtlebot3.git && \
    git clone -b noetic-devel https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git

# Copy the modified turtlebot3 model files
copy turtlebot3_waffle.urdf.xacro /catkin_ws/src/turtlebot3/turtlebot3_description/urdf/
copy turtlebot3_waffle.gazebo.xacro /catkin_ws/src/turtlebot3/turtlebot3_description/urdf/
copy turtlebot3_waffle_pi.urdf.xacro /catkin_ws/src/turtlebot3/turtlebot3_description/urdf/
copy turtlebot3_waffle_pi.gazebo.xacro /catkin_ws/src/turtlebot3/turtlebot3_description/urdf/

workdir /catkin_ws
run /bin/bash -c "source /opt/ros/noetic/setup.bash; cd /catkin_ws; catkin_make"

run echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc && echo "source /catkin_ws/devel/setup.bash" >> ~/.bashrc

env TURTLEBOT3_MODEL=waffle_pi
workdir /
cmd ["bash"]