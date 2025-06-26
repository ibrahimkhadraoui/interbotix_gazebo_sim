# Use the official ROS Melodic desktop full image as base
FROM osrf/ros:noetic-desktop-full-focal

# Set non-interactive frontend for apt
ENV DEBIAN_FRONTEND=noninteractive

# Update and upgrade system
RUN apt-get update && \
    apt-get dist-upgrade -y && \
    rosdep update

RUN apt-get install -y git-all libignition-math4-dev curl figlet net-tools

# Install interbotix dependencies
WORKDIR /home
RUN curl 'https://raw.githubusercontent.com/Interbotix/interbotix_ros_manipulators/main/interbotix_ros_xsarms/install/amd64/xsarm_amd64_install.sh' > xsarm_amd64_install.sh
RUN chmod +x xsarm_amd64_install.sh
RUN ./xsarm_amd64_install.sh -d noetic -p /home/interbotix_ws -n
RUN bash -c "source /opt/ros/noetic/setup.bash && \
    source /home/interbotix_ws/devel/setup.bash"

# Expose the ports for the ROS master
EXPOSE 11311

ENTRYPOINT [ "/ros_entrypoint.sh" ]
CMD [ "/bin/bash" ]
