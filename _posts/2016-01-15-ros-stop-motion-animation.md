---
title: ROS Stop Motion Animation Tools
layout: post
---

<iframe width="560" height="315" src="https://www.youtube.com/embed/mc1xC_bGN5E" frameborder="0" allowfullscreen></iframe>

The key nodes required and very useful to making an animation are mostly here within the vimjay project:
https://github.com/lucasw/vimjay/tree/master/src/standalone

    roslaunch vimjay stop_motion.launch

The key nodes includes a space bar triggering node using OpenCV that connects to a node that saves input images to disk.  The gray window has to be in focus to trigger the animation, but I could make a raw X version that would accept a keypress with any window in focus (which might get counter-intuitive if the user is trying to type something and needs to use the spacebar).

Another node saves a buffer of all the images that have been saved to disk, and constantly publishes an image that shows the full animation. 

The modified v4l2ucp project is used to configure the webcam (and I'd like to continue modifying it to make it fully ros enabled with a separate node for the ui, so a webcam can be configured from a remote machine).

The node most relevant to the vimjay project is the IIR image processing node- it will subscribe to any number of inputs and then combine them with the provided coefficients.  It is actually only FIR filtering currently, a second set of coefficients needs to be supported to allow incorporation of the output frames.  Another mode ought to only subscribe to a single input image and save sufficient older images in a buffer to use them for the coefficients.

In one case the IIR image is emphasizing the difference between the last saved frame and the live image, in the other it is showing the differences by averaging the the same two frames together.  For the diff image, another node generates a plain gray image.
