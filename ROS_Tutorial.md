## Overview

These are notes on using ROS1 or ROS2. The tutorials are based on using the zsh terminal and **NOT bashrc**.

**1. Create workspace**

Initialising ROS1 workspace by `catkin_make`,

Initialising ROS2 workspace by `colcon build --symlink-install`,

if ROS1, initialise ROS1 by `roscore`

1. Declaring devel source file in `.zshrc` or `.bashrc` according to your usage

Example,
```
gedit ~/.zshrc
source ~/opt/ros/<"ros-version">/setup.zsh
```
Realistic example,
```
source ~/opt/ros/noetic/setup.zsh
```
Example:
```
source ~/<"workspace-name">/devel/setup.zsh
```
Realistic Example:
```
source ~/kpt_training/devel/setup.zsh
source ~/.zshrc
```

2. Initialise ROS2 Humble by Docker


```
sudo docker run -p 6080:80 --security-opt seccomp=unconfined --shm-size=512m tiryoh/ros2-desktop-vnc:humble
```
Visit by browser,
```
http://localhost:6080/
```