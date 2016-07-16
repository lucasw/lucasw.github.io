---
title: Kobuki Turtlebot 2 Base with Kinetic
layout: post
---

```
sudo apt-get install ros-kinetic-kobuki
```

```
catkin_make
/bin/sh: 1: pyrcc4: not found
kobuki_desktop/kobuki_qtestsuite/CMakeFiles/kobuki_qtestsuite.dir/build.make:57: recipe for target 'kobuki_desktop/kobuki_qtestsuite/CMakeFiles/kobuki_qtestsuite' failed
make[2]: *** [kobuki_desktop/kobuki_qtestsuite/CMakeFiles/kobuki_qtestsuite] Error 127
CMakeFiles/Makefile2:13443: recipe for target 'kobuki_desktop/kobuki_qtestsuite/CMakeFiles/kobuki_qtestsuite.dir/all' failed
make[1]: *** [kobuki_desktop/kobuki_qtestsuite/CMakeFiles/kobuki_qtestsuite.dir/all] Error 2
make[1]: *** Waiting for unfinished jobs....
```

```
apt-cache search pyrcc4
pyqt4-dev-tools - Development tools for PyQt4
sudo apt-get install pyqt4-dev-tools
```

Looks like following already pull requested at https://github.com/yujinrobot/kobuki_desktop/pull/46/commits

```
                 from /home/lucasw/catkin_ws/src/kobuki_desktop/kobuki_gazebo_plugins/include/kobuki_gazebo_plugins/gazebo_ros_kobuki.h:45,
                 from /home/lucasw/catkin_ws/src/kobuki_desktop/kobuki_gazebo_plugins/src/gazebo_ros_kobuki.cpp:8:
/usr/include/c++/5/bits/c++0x_warning.h:32:2: error: #error This file requires compiler and library support for the ISO C++ 2011 standard. This support must be enabled with the -std=c++11 or -std=gnu++11 compiler options.
 #error This file requires compiler and library support \
```

Add to kobuki_desktop/kobuki_gazebo_plugins
```
set(CMAKE_CXX_FLAGS "-std=c++0x ${CMAKE_CXX_FLAGS}")
```


```
/home/lucasw/catkin_ws/src/kobuki_desktop/kobuki_gazebo_plugins/src/gazebo_ros_kobuki_updates.cpp: In member function ‘void gazebo::GazeboRosKobuki::updateOdometry(gazebo::common::Time&)’:
/home/lucasw/catkin_ws/src/kobuki_desktop/kobuki_gazebo_plugins/src/gazebo_ros_kobuki_updates.cpp:76:15: error: ‘isnan’ was not declared in this scope
   if (isnan(d1))
```

Replace isnan with std::isnan

```
/home/lucasw/catkin_ws/src/kobuki_desktop/kobuki_gazebo_plugins/src/gazebo_ros_kobuki_updates.cpp: In member function ‘void gazebo::GazeboRosKobuki::updateOdometry(gazebo::common::Time&)’:
/home/lucasw/catkin_ws/src/kobuki_desktop/kobuki_gazebo_plugins/src/gazebo_ros_kobuki_updates.cpp:92:24: error: ‘class gazebo::sensors::ImuSensor’ has no member named ‘GetAngularVelocity’
   vel_angular_ = imu_->GetAngularVelocity();
```

Replace with AngularVelocity(), GetOrientation() -> Orientation(), GetLinearAcceleration() -> LinearAcceleration()


```
93: error: no matching function for call to ‘dynamic_pointer_cast(gazebo::sensors::SensorPtr)’
                        sensors::SensorManager::Instance()->GetSensor(cliff_sensor_left_name));
```

Replace boost:: with std:: from dynamic_pointer_cast.


# Real Robot

Don't have an ac adapter, what does it even look like?


Pressed switch to on, hear noise and status led lights up.

Connect usb cable and see

```
Bus 003 Device 002: ID 0403:6001 Future Technology Devices International, Ltd FT232 USB-Serial (UART) IC

```

and /dev/ttyUSB0 has appeared.

```

```

```
roslaunch kobuki_node minimal.launch --screen

... logging to /home/lucasw/.ros/log/f79d7bba-4a25-11e6-bc43-d8fc93bc28de/roslaunch-L007-4784.log
Checking log directory for disk usage. This may take awhile.
Press Ctrl-C to interrupt
Done checking log file disk usage. Usage is <1GB.

started roslaunch server http://127.0.0.1:33194/

SUMMARY
========

PARAMETERS
 * /diagnostic_aggregator/analyzers/input_ports/contains: ['Digital Input',...
 * /diagnostic_aggregator/analyzers/input_ports/path: Input Ports
 * /diagnostic_aggregator/analyzers/input_ports/remove_prefix: mobile_base_nodel...
 * /diagnostic_aggregator/analyzers/input_ports/timeout: 5.0
 * /diagnostic_aggregator/analyzers/input_ports/type: diagnostic_aggreg...
 * /diagnostic_aggregator/analyzers/kobuki/contains: ['Watchdog', 'Mot...
 * /diagnostic_aggregator/analyzers/kobuki/path: Kobuki
 * /diagnostic_aggregator/analyzers/kobuki/remove_prefix: mobile_base_nodel...
 * /diagnostic_aggregator/analyzers/kobuki/timeout: 5.0
 * /diagnostic_aggregator/analyzers/kobuki/type: diagnostic_aggreg...
 * /diagnostic_aggregator/analyzers/power/contains: ['Battery']
 * /diagnostic_aggregator/analyzers/power/path: Power System
 * /diagnostic_aggregator/analyzers/power/remove_prefix: mobile_base_nodel...
 * /diagnostic_aggregator/analyzers/power/timeout: 5.0
 * /diagnostic_aggregator/analyzers/power/type: diagnostic_aggreg...
 * /diagnostic_aggregator/analyzers/sensors/contains: ['Cliff Sensor', ...
 * /diagnostic_aggregator/analyzers/sensors/path: Sensors
 * /diagnostic_aggregator/analyzers/sensors/remove_prefix: mobile_base_nodel...
 * /diagnostic_aggregator/analyzers/sensors/timeout: 5.0
 * /diagnostic_aggregator/analyzers/sensors/type: diagnostic_aggreg...
 * /diagnostic_aggregator/base_path: 
 * /diagnostic_aggregator/pub_rate: 1.0
 * /mobile_base/base_frame: base_footprint
 * /mobile_base/battery_capacity: 16.5
 * /mobile_base/battery_dangerous: 13.2
 * /mobile_base/battery_low: 14.0
 * /mobile_base/cmd_vel_timeout: 0.6
 * /mobile_base/device_port: /dev/kobuki
 * /mobile_base/odom_frame: odom
 * /mobile_base/publish_tf: True
 * /mobile_base/use_imu_heading: True
 * /mobile_base/wheel_left_joint_name: wheel_left_joint
 * /mobile_base/wheel_right_joint_name: wheel_right_joint
 * /rosdistro: kinetic
 * /rosversion: 1.12.2

NODES
  /
    diagnostic_aggregator (diagnostic_aggregator/aggregator_node)
    mobile_base (nodelet/nodelet)
    mobile_base_nodelet_manager (nodelet/nodelet)

ROS_MASTER_URI=http://127.0.0.1:11311

setting /run_id to f79d7bba-4a25-11e6-bc43-d8fc93bc28de
core service [/rosout] found
process[mobile_base_nodelet_manager-1]: started with pid [4804]
process[mobile_base-2]: started with pid [4805]
process[diagnostic_aggregator-3]: started with pid [4806]
[ INFO] [/mobile_base] [/tmp/binarydeb/ros-kinetic-nodelet-1.9.4/src/nodelet.cpp]:[195] [Loading nodelet /mobile_base of type kobuki_node/KobukiNodelet to manager mobile_base_nodelet_manager with the following remappings:]
[ INFO] [/mobile_base] [/tmp/binarydeb/ros-kinetic-nodelet-1.9.4/src/nodelet.cpp]:[201] [/mobile_base/joint_states -> /joint_states]
[ INFO] [/mobile_base] [/tmp/binarydeb/ros-kinetic-nodelet-1.9.4/src/nodelet.cpp]:[201] [/mobile_base/odom -> /odom]
[ INFO] [/mobile_base] [/tmp/binarydeb/ros-kinetic-roscpp-1.12.2/src/libros/service.cpp]:[80] [waitForService: Service [/mobile_base_nodelet_manager/load_nodelet] has not been advertised, waiting...]
[ INFO] [/mobile_base_nodelet_manager] [/tmp/binarydeb/ros-kinetic-nodelet-1.9.4/src/loader.cpp]:[221] [Initializing nodelet with 8 worker threads.]
[ INFO] [/mobile_base] [/tmp/binarydeb/ros-kinetic-roscpp-1.12.2/src/libros/service.cpp]:[122] [waitForService: Service [/mobile_base_nodelet_manager/load_nodelet] is now available.]
[ WARN] [/mobile_base_nodelet_manager] [/tmp/binarydeb/ros-kinetic-kobuki-node-0.7.0/src/library/kobuki_ros.cpp]:[162] [Kobuki : no robot description given on the parameter server]
[ INFO] [/mobile_base_nodelet_manager] [/tmp/binarydeb/ros-kinetic-kobuki-node-0.7.0/src/library/kobuki_ros.cpp]:[198] [Kobuki : configured for connection on device_port /dev/kobuki [/mobile_base].]
[ INFO] [/mobile_base_nodelet_manager] [/tmp/binarydeb/ros-kinetic-kobuki-node-0.7.0/src/library/kobuki_ros.cpp]:[199] [Kobuki : driver running in normal (non-simulation) mode [/mobile_base].]
[ INFO] [/mobile_base_nodelet_manager] [/tmp/binarydeb/ros-kinetic-kobuki-node-0.7.0/src/library/odometry.cpp]:[37] [Kobuki : Velocity commands timeout: 0.600000000 seconds [/mobile_base].]
[ INFO] [/mobile_base_nodelet_manager] [/tmp/binarydeb/ros-kinetic-kobuki-node-0.7.0/src/library/odometry.cpp]:[42] [Kobuki : using odom_frame [odom][/mobile_base].]
[ INFO] [/mobile_base_nodelet_manager] [/tmp/binarydeb/ros-kinetic-kobuki-node-0.7.0/src/library/odometry.cpp]:[48] [Kobuki : using base_frame [base_footprint][/mobile_base].]
[ INFO] [/mobile_base_nodelet_manager] [/tmp/binarydeb/ros-kinetic-kobuki-node-0.7.0/src/library/odometry.cpp]:[55] [Kobuki : publishing transforms [/mobile_base].]
[ INFO] [/mobile_base_nodelet_manager] [/tmp/binarydeb/ros-kinetic-kobuki-node-0.7.0/src/library/odometry.cpp]:[65] [Kobuki : using imu data for heading [/mobile_base].]
[ WARN] [/mobile_base_nodelet_manager] [/tmp/binarydeb/ros-kinetic-kobuki-node-0.7.0/include/kobuki_node/kobuki_ros.hpp]:[176] [Kobuki : device does not (yet) available, is the usb connected?.]
[ INFO] [/mobile_base_nodelet_manager] [/tmp/binarydeb/ros-kinetic-kobuki-node-0.7.0/include/kobuki_node/kobuki_ros.hpp]:[175] [Kobuki : device does not (yet) available on this port, waiting...]
[ WARN] [/mobile_base_nodelet_manager] [/tmp/binarydeb/ros-kinetic-kobuki-node-0.7.0/src/library/kobuki_ros.cpp]:[213] [Kobuki : no data stream, is kobuki turned on?]
[ INFO] [/mobile_base_nodelet_manager] [/tmp/binarydeb/ros-kinetic-kobuki-node-0.7.0/src/nodelet/kobuki_nodelet.cpp]:[67] [Kobuki : initialised.]
[ INFO] [/mobile_base_nodelet_manager] [/tmp/binarydeb/ros-kinetic-kobuki-node-0.7.0/include/kobuki_node/kobuki_ros.hpp]:[175] [Kobuki : device does not (yet) available on this port, waiting...]
[ INFO] [/mobile_base_nodelet_manager] [/tmp/binarydeb/ros-kinetic-kobuki-node-0.7.0/include/kobuki_node/kobuki_ros.hpp]:[175] [Kobuki : device does not (yet) available on this port, waiting...]
[ INFO] [/mobile_base_nodelet_manager] [/tmp/binarydeb/ros-kinetic-kobuki-node-0.7.0/include/kobuki_node/kobuki_ros.hpp]:[175] [Kobuki : device does not (yet) available on this port, waiting...]
[ INFO] [/mobile_base_nodelet_manager] [/tmp/binarydeb/ros-kinetic-kobuki-node-0.7.0/include/kobuki_node/kobuki_ros.hpp]:[175] [Kobuki : device does not (yet) available on this port, waiting...]
[ INFO] [/mobile_base_nodelet_manager] [/tmp/binarydeb/ros-kinetic-kobuki-node-0.7.0/include/kobuki_node/kobuki_ros.hpp]:[175] [Kobuki : device does not (yet) available on this port, waiting...]
[ INFO] [/mobile_base_nodelet_manager] [/tmp/binarydeb/ros-kinetic-kobuki-node-0.7.0/include/kobuki_node/kobuki_ros.hpp]:[175] [Kobuki : device does not (yet) available on this port, waiting...]
[ INFO] [/mobile_base_nodelet_manager] [/tmp/binarydeb/ros-kinetic-kobuki-node-0.7.0/include/kobuki_node/kobuki_ros.hpp]:[175] [Kobuki : device does not (yet) available on this port, waiting...]
[ INFO] [/mobile_base_nodelet_manager] [/tmp/binarydeb/ros-kinetic-kobuki-node-0.7.0/include/kobuki_node/kobuki_ros.hpp]:[175] [Kobuki : device does not (yet) available on this port, waiting...]
```

Then battery died :(
