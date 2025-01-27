FROM ubuntu:jammy

RUN locale  # check for UTF-8
RUN apt update && apt install locales -y
RUN locale-gen it_IT it_IT.UTF-8
RUN update-locale LC_ALL=it_IT.UTF-8 LANG=it_IT.UTF-8
RUN export LANG=it_IT.UTF-8

# Set the timezone
ENV ROS_VERSION=2
ENV ROS_DISTRO=humble
ENV ROS_PYTHON_VERSION=3
ENV TZ=Europe/Rome
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt install software-properties-common
RUN add-apt-repository universe

RUN apt update && apt upgrade -y

RUN apt install ros-humble-ros-base -y
RUN apt install ros-dev-tools -y

RUN apt-get install -y python3-colcon-common-extensions 
RUN apt-get install -y ros-humble-rviz2
RUN apt-get install -y ros-humble-controller-manager
RUN apt-get install -y ros-humble-robot-state-publisher
RUN apt-get install -y ros-humble-joint-state-publisher
RUN apt-get install -y ros-humble-joint-state-publisher-gui
RUN apt-get install -y ros-humble-gazebo-ros-pkgs
RUN apt-get install -y ros-humble-trajectory-msgs
RUN apt-get install -y ros-humble-velocity-controllers
RUN apt-get install -y ros-humble-joint-trajectory-controller
RUN apt-get install -y ros-humble-gazebo-ros2-control-demos
RUN apt-get install -y ros-humble-teleop-tools 
RUN apt-get install -y ros-humble-key-teleop
RUN apt-get install -y ros-humble-tf-transformations
RUN apt-get install -y ros-humble-xacro    

# Install Git
RUN apt install -y git

# Rosdep update
RUN rosdep update

# Source the ROS setup file
RUN echo "source /opt/ros/${ROS_DISTRO}/setup.bash" >> ~/.bashrc

################################
## ADD ANY CUSTOM SETUP BELOW ##
################################

RUN mkdir -p /workspace 

WORKDIR /workspace

COPY entrypoint.sh /entrypoint.sh
COPY bashrc /home/root/.bashrc


# Set up entrypoint and default command
ENTRYPOINT ["/bin/bash", "/entrypoint.sh"] 
CMD ["bash"]

RUN git clone https://github.com/SupaeroMoon-ERC-MDRS/OBC-MDRS-RPI.git

EXPOSE 12121/udp
EXPOSE 13000/udp
EXPOSE 13000/tcp



