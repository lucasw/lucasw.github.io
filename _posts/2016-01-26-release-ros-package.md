---
title: ROS Stop Motion Animation Tools
layout: post
---

Tried prepare release:

    $ catkin_prepare_release 
    Prepare the source repository for a release.
    Repository type: git
    No packages found

This was because the package name and the repository name did not match.
It is nice to have 'ros' in the repo name, but seems redundant in the package name, but I went with renaming screengrab_ros to screen_grab.
