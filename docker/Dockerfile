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
    lsb-release \
    iputils-ping


RUN echo "set -g mouse on" > /root/.tmux.conf

# Mavlink
RUN apt-get update && apt-get install ros-noetic-mavros ros-noetic-mavros-extras
RUN wget https://raw.githubusercontent.com/mavlink/mavros/master/mavros/scripts/install_geographiclib_datasets.sh \
    && chmod a+x install_geographiclib_datasets.sh \
    && ./install_geographiclib_datasets.sh \
    && rm install_geographiclib_datasets.sh

# Realsense
RUN sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE
RUN sudo add-apt-repository "deb https://librealsense.intel.com/Debian/apt-repo $(lsb_release -cs) main" -u
RUN sudo apt-get update && sudo apt-get install librealsense2-dkms \
                                                librealsense2-utils \
                                                librealsense2-dbg \
                                                librealsense2-dev \
                                                ros-noetic-realsense2-camera

# Optitrack
RUN sudo apt-get install ros-noetic-vrpn-client-ros

# Indicate that we are inside a drone
RUN echo "PS1='🚁 🤖'\${PS1}" >> /root/.bashrc

RUN echo "source /opt/ros/noetic/setup.bash" >> /root/.bashrc

RUN rm -rf log # remove log folder

WORKDIR /root/