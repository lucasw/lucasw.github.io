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



