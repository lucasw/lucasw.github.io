---
layout: post
title: ROS Blockly
---

The reason that Erle forked blockly is because their custom blockly blocks are stored in it.
There ought to be a way to put these in ros_blockly, and for any I or anyone else creates in a third repo.

Make a custom js file to provide std_msgs- start with an Empty.
cp erle-spider.js and make an Empty publisher.

  Blockly.Blocks['std_msgs_empty'] = {
    init: function() {
      this.appendDummyInput()
          .appendField("Empty");
      this.setPreviousStatement(true);
      this.setNextStatement(true);
      this.setColour(260);
      this.setTooltip('Publish an Empty');
      this.setHelpUrl('http://lucasw.github.io/');
    }
  };

So is anything special needed to make blockly aware of this new file?
`frontend/blockly/generators/python/erle-spider.js` has the implementation.
It's a little ugly to write python in javascript- having individual python files loaded into js would be cleaner.


  'use strict';

  goog.provide('Blockly.Python.spider');
  goog.require('Blockly.Python');

  Blockly.Python['std_msgs_empty'] = function(block) {
    // var code = 'print "standing up..."\n';
    var code = ""
    code+="import sys\n"
    code+="import time\n"
    code+="from std_msgs.msg import Empty\n"
    code+="\n"
    code+="################\n"
    code+="## INITIALIZE ##\n"
    code+="################ \n"
    /** TODO(lucasw) Need to have the the block proved a name parameter */
    code+="pub = rospy.Publisher('/empty', Empty, queue_size=10)\n"
    code+="msg = Empty()\n"
    code+="i = 0\n"
    code+="rate = rospy.Rate(10)\n"
    code+="\n"
    code+="####################\n"
    code+="## EMPTY         ##\n"
    code+="####################\n"
    code+="while not rospy.is_shutdown() and i < 10:\n"
    code+=" pub.publish(msg)\n"
    code+=" rate.sleep()\n"
    code+=" i += 1\n"
    code+="time.sleep(2)\n"

    return code;
  };

Now try to restart front end to support this.
ctrl-c doesn't work.
backend node doesn't show up on rosnode list.
Just `ps aux | grep blockly` and then `kill -9` it.

Tried restarting it, then refreshing http://localhost/ros_blockly, but don't see anything different.
Not sure about blockly_compressed.js - do I need to regenerate that?
There are a lot of references to it in other js files.
Look at blockly/build.py
Tried running it and it mostly changed blockly_uncompressed.js.

  # The compressed file is a concatenation of all of Blockly's core files which
  # have been run through Google's Closure Compiler.  This is done using the
  # online API (which takes a few seconds and requires an Internet connection).

Don't have an internet connection currently which is why this didn't work.
