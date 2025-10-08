FROM osrf/ros:humble-desktop-full

SHELL [ "/bin/bash" , "-c" ]

# Upgrade all packages
RUN sudo apt update && sudo apt upgrade -y

# Install essential packages
RUN sudo apt install -y \
    wget \
    usbutils

# Install essential ROS components
RUN sudo apt install -y \
    ros-${ROS_DISTRO}-sensor-msgs

# Create overlay workspace
WORKDIR /root/ros_ws/src
COPY packages.repos .

RUN vcs import < packages.repos; \
    cd ..; \
    rosdep install --from-paths src --ignore-src -r -y; \
    source /opt/ros/${ROS_DISTRO}/setup.bash; \
    colcon build;

# Add sourcing ROS setup.bash to .bashrc
RUN echo "source /opt/ros/${ROS_DISTRO}/setup.bash" >> ~/.bashrc
RUN echo "source ~/.bashrc"