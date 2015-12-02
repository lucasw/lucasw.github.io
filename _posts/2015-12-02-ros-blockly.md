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
      File "/home/lwalter/ros_catkin_ws/src/ros_blockly/scripts/blockly_backend.py", line 137, in <module>
        talker()
      File "/home/lwalter/ros_catkin_ws/src/ros_blockly/scripts/blockly_backend.py", line 119, in talker
        factory.protocol = BlocklyServerProtocol
    NameError: name 'BlocklyServerProtocol' is not defined

So something is wrong, maybe do need install?
