FROM osrf/ros:kinetic-desktop-full-xenial

ARG USERNAME=yutou
ARG USER_UID=1000
ARG USER_GID=1000

# Install basic tools and dependencies
RUN apt-get update && \
    apt-get install -y \
    nautilus \
    gedit \
    cmake \
    git \
    libboost-all-dev \
    build-essential \
    libtbb-dev && \
    rm -rf /var/lib/apt/lists/*

# Add GTSAM PPA repository and install
RUN apt-get update && \
    apt-get install -y software-properties-common && \
    add-apt-repository ppa:borglab/gtsam-release-4.0  -y && \
    add-apt-repository ppa:borglab/gtsam-develop -y && \
    apt-get update && \
    apt-get install -y libgtsam-dev libgtsam-unstable-dev && \
    rm -rf /var/lib/apt/lists/*

# Create user and configure sudo privileges
RUN groupadd --gid $USER_GID $USERNAME && \
    useradd --uid $USER_UID --gid $USER_GID -m $USERNAME && \
    apt-get update && \
    apt-get install -y sudo && \
    echo "$USERNAME ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

USER $USERNAME
WORKDIR /home/$USERNAME

# Configure bashrc
RUN echo "source /opt/ros/kinetic/setup.bash" >> /home/$USERNAME/.bashrc && \
    echo "source /home/yutou/ros_ws/devel/setup.bash" >> /home/$USERNAME/.bashrc

CMD ["/bin/bash"]