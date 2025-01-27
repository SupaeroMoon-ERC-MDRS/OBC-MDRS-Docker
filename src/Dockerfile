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

RUN apt install software-properties-common -y
RUN add-apt-repository universe -y

RUN apt update && apt install curl -y
RUN curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg

RUN echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | tee /etc/apt/sources.list.d/ros2.list > /dev/null

RUN apt update && apt upgrade -y

RUN apt install ros-humble-ros-base -y
RUN apt install ros-dev-tools -y

RUN apt-get install -y python3-colcon-common-extensions 
RUN apt-get install -y ros-humble-rviz2
RUN apt-get install -y ros-humble-controller-manager
RUN apt-get install -y ros-humble-robot-state-publisher
RUN apt-get install -y ros-humble-joint-state-publisher
RUN apt-get install -y ros-humble-joint-state-publisher-gui
RUN apt-get install -y ros-humble-trajectory-msgs
RUN apt-get install -y ros-humble-velocity-controllers
RUN apt-get install -y ros-humble-joint-trajectory-controller
RUN apt-get install -y ros-humble-teleop-tools 
RUN apt-get install -y ros-humble-key-teleop
RUN apt-get install -y ros-humble-tf-transformations
RUN apt-get install -y ros-humble-xacro
RUN apt-get install python3-rosdep

# Install Git
RUN apt install -y git

# Rosdep update
# RUN rosdep init
# RUN rosdep update

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



