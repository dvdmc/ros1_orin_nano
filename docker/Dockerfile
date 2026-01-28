FROM ros:noetic-ros-base

SHELL ["/bin/bash", "-c"]

RUN apt-get update && apt-get upgrade -y \
  && apt-get install -y \
    tmux \
    tmuxinator \
    vim \
    xterm \
    ssh \
    tree \
    python3-tk \
    nano \
    libtool \
    libtool-bin \
    htop \
    gdb \
    net-tools \
    cmake \
    software-properties-common \
    lsb-release \
    curl \
    iputils-ping


RUN echo "set -g mouse on" > /root/.tmux.conf

# Mavlink
RUN apt-get install -y ros-noetic-mavros ros-noetic-mavros-extras
RUN wget https://raw.githubusercontent.com/mavlink/mavros/master/mavros/scripts/install_geographiclib_datasets.sh \
    && chmod a+x install_geographiclib_datasets.sh \
    && ./install_geographiclib_datasets.sh \
    && rm install_geographiclib_datasets.sh

# Realsense
RUN mkdir -p /etc/apt/keyrings && \
    curl -sSf https://librealsense.intel.com/Debian/librealsense.pgp | tee /etc/apt/keyrings/librealsense.pgp > /dev/null
RUN echo "deb [signed-by=/etc/apt/keyrings/librealsense.pgp] https://librealsense.intel.com/Debian/apt-repo `lsb_release -cs` main" | \
    tee /etc/apt/sources.list.d/librealsense.list
RUN apt-get update && apt-get install -y \
    librealsense2-utils \
    librealsense2-dbg \
    librealsense2-dev \
    ros-noetic-realsense2-camera

# Optitrack
RUN apt-get install -y ros-noetic-vrpn-client-ros

# Optitrack arena (Unizar package)
COPY ./optitrack_arena /root/optitrack_ws/src/optitrack_arena
WORKDIR /root/optitrack_ws
RUN apt-get update && apt-get install -y python3-catkin-tools ros-noetic-tf2-sensor-msgs ros-noetic-tf2-geometry-msgs
RUN source /opt/ros/noetic/setup.bash && catkin build

# PTZ
# RUN apt-get install -y ros-noetic-ptz

# Other ROS packages
RUN apt-get install -y ros-noetic-rqt-tf-tree

# Indicate that we are inside a drone
RUN echo "PS1='🚁 🤖 🐋 '\${PS1}" >> /root/.bashrc

RUN echo "source /opt/ros/noetic/setup.bash" >> /root/.bashrc
RUN echo "source /root/optitrack_ws/devel/setup.bash" >> /root/.bashrc

RUN rm -rf log # remove log folder

WORKDIR /root/
