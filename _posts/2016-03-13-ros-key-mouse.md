---
layout: post
title: ROS messages for keyboard and mice, and generating key and mouse events at X11 level
---

http://answers.ros.org/question/228956/node-that-generates-key-or-mouse-events-at-low-level/

It seems like there ought to be sensor_msgs/Mouse and sensor_msgs/Key.
With those existing, no node (mainly teleop nodes) ought to read the keyboard directly just listen to that message type and have a default keyboard reading node that generates it.

Any node that reads a key, mouse, or joystick, or some other specialized input (that does not map to a sensor_msgs/Joy?), ought to have a standard way of being reconfigured, of any button being mapped to any function that would otherwise be hardcoded.

Furthermore a keyboard, mouse, and joystick ought to have interchangeability, maybe via custom nodes (that would use the above standard remapping).
A joystick could be mapped to a mouse, or vice versa, or generate keyboard events.

sensor_msgs/Joy messages are stamped, so likewise with the mouse and keyboard.
Would some node do tf lookups on those inputs, to decide that a certain command was meant for a certain state at a certain past time, but still has the job of taking that intended action and updating it for the present state.

The above ought to be possible all within ros messages.

# Generating events at sub-ROS level

But a second under layer is needed for interacting with ros nodes that do not conform to the standard of using the basic message types, or non ros applications that can only be interacted with mouse/keyboard/joystick.

(Just like there ought to be a way to publish a ros image into a v4l2 video)

/dev/input/mouseN vs. /dev/input/mice -> support any number of mouses.

Most likely this would mean generating synthetic X11 events.

http://www.doctort.org/adam/nerd-notes/x11-fake-keypress-event.html

libxdo and xdotool

python-xdo ('Only a small part of the library is supported' - so python version is not ideal)

https://github.com/ros-visualization/robhum_ui_utils/tree/master/virtual_keyboard

https://github.com/lucasw/xdo_ros


How to show full keyboard in ubuntu, what buttons are being pressed.
key-mon just shows the most recent key down.
gkb-keyboard-display -l us
This works though is a little big, cannot be resized.
Also does not show keypresses when out of focus, but still useful for debugging the key/up downs.
