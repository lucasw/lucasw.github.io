---
layout: post
title: ROS Blockly
---

Following the install instructions from [ros blockly](http://wiki.ros.org/blockly).
It is weird to clone inside of other directories, I guess it is enforcing relative paths.

It looks like Erle has forked blockly, why is that?

ace-build is a javascript code editor, also forked.
Maybe they don't want changes breaking their blockly stuff?

There is a line which calls for running `deploy.sh`, inside there is just one line to copy the entire contents of frontend to /var/www/html.
Instead make a symlink to frontend:

    /var/www$ sudo ln -s /home/lucasw/ros_catkin_ws/src/ros_blockly/frontend/ ros_blockly

Then can go to [localhost blockly](http://localhost/ros_blockly/pages/blockly.html)

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

Typo, BLockly -> Blockly in blockly_backend.py.
[erle ros blockly](https://github.com/erlerobot/ros_blockly/pull/12)

Now look at webpage again, refresh it.

See this output from backend rosrun:

   Client connecting: tcp:127.0.0.1:51351
   WebSocket connection open.

Now there is a /blockly topic of type String.

Try creating something - a while loop that does 'Go forward 2 seconds'.
Then press launch.

On backend console:

    Text message received: for count in range(10):
      import sys
      import time
      from crab_msgs.msg import *
      from sensor_msgs.msg import Joy

      walking_time=2

      ################
      ## INITIALIZE ##
      ################
      pub = rospy.Publisher('/joy', Joy, queue_size=10)
      msg = Joy()
      msg.header.stamp = rospy.Time.now()
      rate = rospy.Rate(10)

      valueAxe = 0.0
      valueButton = 0
      for i in range (0, 20):
        msg.axes.append(valueAxe)
      for e in range (0, 17):
        msg.buttons.append(valueButton)


      #################
      ## FORWARD  ##
      #################
      start = time.time()
      msg.axes[1] =  1
      bo=True
      while not rospy.is_shutdown() and bo:
        sample_time = time.time()
        if ((sample_time - start) > walking_time):
          bo=False
          msg.axes[1] = 0
        pub.publish(msg)
        rate.sleep()

    building the ros node...
    The file generated contains...
    #!/usr/bin/env python3
    import rospy
    from std_msgs.msg import String

    rospy.init_node('blockly_node', anonymous=True)
    for count in range(10):
      import sys
      import time
      from crab_msgs.msg import *
      from sensor_msgs.msg import Joy

      walking_time=2

      ################
      ## INITIALIZE ##
      ################
      pub = rospy.Publisher('/joy', Joy, queue_size=10)
      msg = Joy()
      msg.header.stamp = rospy.Time.now()
      rate = rospy.Rate(10)

      valueAxe = 0.0
      valueButton = 0
      for i in range (0, 20):
        msg.axes.append(valueAxe)
      for e in range (0, 17):
        msg.buttons.append(valueButton)


      #################
      ## FORWARD  ##
      #################
      start = time.time()
      msg.axes[1] =  1
      bo=True
      while not rospy.is_shutdown() and bo:
        sample_time = time.time()
        if ((sample_time - start) > walking_time):
          bo=False
          msg.axes[1] = 0
        pub.publish(msg)
        rate.sleep()


    Traceback (most recent call last):
      File "test.py", line 9, in <module>
        from crab_msgs.msg import *
    ImportError: No module named 'crab_msgs'


But I didn't see anything from a `rostopic echo /blockly`.

Don't have crab_msgs, what about making custom message using basic String/Float/Bool types?


## Try out install


    catkin_make_isolated --pkg blockly --install

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
