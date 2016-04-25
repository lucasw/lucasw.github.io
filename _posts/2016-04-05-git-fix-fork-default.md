---
layout: post
title: git fix fork master
---


Was lazy about forking a repo and then making local changes to default branch, now want all changes that correspond to issues/pull request to go into uniquely named branches, and have the default branch track the upstream repo.

```
git remote add upstream https://github.com/ros-simulation/gazebo_ros_pkgs.git
git remote -v
origin  https://github.com/lucasw/gazebo_ros_pkgs.git (fetch)
origin  https://github.com/lucasw/gazebo_ros_pkgs.git (push)
upstream  https://github.com/ros-simulation/gazebo_ros_pkgs.git (fetch)
upstream  https://github.com/ros-simulation/gazebo_ros_pkgs.git (push)

# was this because I tried to delete it?
git checkout jade-devel
error: pathspec 'jade-devel' did not match any file(s) known to git.

git branch jade-devel

git checkout jade-devel
Switched to branch 'jade-devel'

git fetch upstream
git reset --hard upstream/jade-devel

git push origin jade-devel
Username for 'https://github.com': lucasw
Password for 'https://lucasw@github.com': 
To https://github.com/lucasw/gazebo_ros_pkgs.git
! [rejected]        jade-devel -> jade-devel (non-fast-forward)
error: failed to push some refs to 'https://github.com/lucasw/gazebo_ros_pkgs.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

git push -f origin jade-devel
Username for 'https://github.com': lucasw
Password for 'https://lucasw@github.com': 
Total 0 (delta 0), reused 0 (delta 0)
To https://github.com/lucasw/gazebo_ros_pkgs.git
 + 7ba4409...c190bf6 jade-devel -> jade-devel (forced update)
```
