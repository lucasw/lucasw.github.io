---
title: ROS Kinetic with Gazebo
layout: post
---

Clean install of Ubuntu 16.04 and ROS Kinetic.

carbot ( http://github.com/lucasw/carbot.git ) project runs fine.

if `libgazebo_ros_control.so` isn't present then loading controllers fails without recognizing that is why, need to install it from source currently:

```
git clone -b kinetic-devel https://github.com/ros-simulation/gazebo_ros_pkgs.git
```

Also need to git clone teleop twist joy package, but haven't done that because trying out keyboard twist generator (the scale factor needs to be turned down, assuming there is one, also not sure if I like the keyboard approach in it).


```
sudo apt-get install ros-kinetic-controller-manager ros-kinetic-controller-manager ros-kinetic-control-toolbox ros-kinetic-gazebo-ros ros-kinetic-joint ros-kinetic-transmission-interface ros-kinetic-joint ros-kinetic-joint-limits-interface ros-kinetic-ros-controllers
```

gazebo 7 looks nicer- the shading is fixed, flat boxes now have normals that aren't the average of adjacent right angle surfaces, the cylinders don't have a strange alternating shade pattern.

Still takes a long time to start- for some reason the first start is extra long.

gazebo still shuts down poorly:

```
^C[acker-10] killing on exit
[cmd_vel_to_joint-9] killing on exit
[rviz-7] killing on exit
[robot_state_publisher-6] killing on exit
[joint_state_publisher-5] killing on exit
[gazebo_gui-4] killing on exit
[gazebo-3] killing on exit
[carbot/spawner-2] killing on exit
[INFO] [245.241000] /opt/ros/kinetic/lib/controller_manager/spawner 58: Shutting down spawner. Stopping and unloading controllers...
[INFO] [245.242000] /opt/ros/kinetic/lib/controller_manager/spawner 71: Stopping all controllers...
[gazebo-3] escalating to SIGTERM
[carbot/spawner-2] escalating to SIGTERM
[WARN] [245.242000] /opt/ros/kinetic/lib/controller_manager/spawner 79: Controller Spawner couldn't reach controller_manager to take down controllers. Waited for 30 second(s).
[rosout-1] killing on exit
[master] killing on exit
shutting down processing monitor...
... shutting down processing monitor complete
done
```
