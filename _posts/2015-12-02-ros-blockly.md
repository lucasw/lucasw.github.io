---
layout: post
title: ROS Blockly
---

Following the install instructions from http://wiki.ros.org/blockly.
It is weird to clone inside of other directories, I guess it is enforcing relative paths.

It looks like Erle has forked blockly, why is that?

ace-build is a javascript code editor, also forked.
Maybe they don't want changes breaking their blockly stuff?

There is a line which calls for running `deploy.sh`, inside there is just one line to copy the entire contents of frontend to /var/www/html.
Instead make a symlink to frontend:

    /var/www$ sudo ln -s /home/lucasw/ros_catkin_ws/src/ros_blockly/frontend/ ros_blockly

Then can go to http://localhost/ros_blockly/pages/blockly.html


Next get the backend:


    sudo apt-get install python3-pip

What is autobahn?
It implements websocket, 'WebSocket allows bidirectional real-time messaging on the Web while WAMP provides applications with high-level communication abstractions (remote procedure calling and publish/subscribe) in an open standard WebSocket-based protocol.'

I'm guessing this helps connect blockly to ros, so they aren't using rosbridge?

It's seems unnecessary to run catkin_make isolated, regular catkin_make is fine.

repo is called ros_blockly but package name is actually blockly.

    roscore
    rosrun blockly blockly_backend.py

    Traceback (most recent call last):
      File "/home/lucasw/ros_catkin_ws/src/ros_blockly/scripts/blockly_backend.py", line 137, in <module>
        talker()
      File "/home/lucasw/ros_catkin_ws/src/ros_blockly/scripts/blockly_backend.py", line 119, in talker
        factory.protocol = BlocklyServerProtocol
    NameError: name 'BlocklyServerProtocol' is not defined

So something is wrong, maybe do need install?


    ==> Processing catkin package: 'blockly'
    ==> Building with env: '/home/lucasw/ros_catkin_ws/install_isolated/env.sh'
    ==> cmake /home/lucasw/ros_catkin_ws/src/ros_blockly -DCATKIN_DEVEL_PREFIX=/home/lucasw/ros_catkin_ws/devel_isolated/blockly -DCMAKE_INSTALL_PREFIX=/home/lucasw/ros_catkin_ws/install_isolated -G Unix Makefiles in '/home/lucasw/ros_catkin_ws/build_isolated/blockly'
    Unhandled exception of type 'OSError':
    Traceback (most recent call last):
      File "/opt/ros/jade/lib/python2.7/dist-packages/catkin/builder.py", line 965, in build_workspace_isolated
        number=index + 1, of=len(ordered_packages)
      File "/opt/ros/jade/lib/python2.7/dist-packages/catkin/builder.py", line 665, in build_package
        destdir=destdir, use_ninja=use_ninja
      File "/opt/ros/jade/lib/python2.7/dist-packages/catkin/builder.py", line 397, in build_catkin_package
        run_command_colorized(cmake_cmd, build_dir, quiet, add_env=add_env)
      File "/opt/ros/jade/lib/python2.7/dist-packages/catkin/builder.py", line 187, in run_command_colorized
        run_command(cmd, cwd, quiet=quiet, colorize=True, add_env=add_env)
      File "/opt/ros/jade/lib/python2.7/dist-packages/catkin/builder.py", line 205, in run_command
        raise OSError("Failed command '%s': %s" % (cmd, e))
    OSError: Failed command '['/home/lucasw/ros_catkin_ws/install_isolated/env.sh', 'cmake', '/home/lucasw/ros_catkin_ws/src/ros_blockly', '-DCATKIN_DEVEL_PREFIX=/home/lucasw/ros_catkin_ws/devel_isolated/blockly', '-DCMAKE_INSTALL_PREFIX=/home/lucasw/ros_catkin_ws/install_isolated', '-G', 'Unix Makefiles']': [Errno 2] No such file or directory
    <== Failed to process package 'blockly': 
      Failed command '['/home/lucasw/ros_catkin_ws/install_isolated/env.sh', 'cmake', '/home/lucasw/ros_catkin_ws/src/ros_blockly', '-DCATKIN_DEVEL_PREFIX=/home/lucasw/ros_catkin_ws/devel_isolated/blockly', '-DCMAKE_INSTALL_PREFIX=/home/lucasw/ros_catkin_ws/install_isolated', '-G', 'Unix Makefiles']': [Errno 2] No such file or directory
    Command failed, exiting.
