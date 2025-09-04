# to run, use 
# docker build -t cs3891:barebones .
# docker run --mount type=bind,source=.,target=/ros/catkin_ws -it cs3891:barebones

# syntax=docker/dockerfile:1
FROM ros:noetic-robot

# change the default shell command
SHELL ["/bin/bash", "-c"] 

# this gets run in this image
RUN source ros_entrypoint.sh

# now add this to all future calls
RUN echo "source /ros_entrypoint.sh" >> /etc/bash.bashrc
RUN echo "set +e" >> /etc/bash.bashrc

# clone the packages we need
# get the git package
RUN apt-get -y update
RUN apt-get -y install git

# change to our working directory
WORKDIR /ros/catkin_ws/

# RUN source /ros_entrypoint.sh && catkin_make

# you only get one command
# CMD roscore

