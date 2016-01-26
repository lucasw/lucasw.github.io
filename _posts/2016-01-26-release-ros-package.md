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

Now it works:

    ~/catkin_ws/src/screen_grab$ catkin_prepare_release
    Prepare the source repository for a release.
    Repository type: git
    Found packages: screen_grab
    Prepare release of version '0.0.2' [Y/n]?
    Trying to push to remote repository (dry run)...
    Username for 'https://github.com': lucasw
    Password for 'https://lucasw@github.com':
    Everything up-to-date
    Checking if working copy is clean (no staged changes, no modified files, no untracked files)...
    Rename the forthcoming section of the following packages to version '0.0.2': screen_grab
    Bump version of all packages from '0.0.1' to '0.0.2'
    Committing the package.xml files...
    [master 69c167d] 0.0.2
     2 files changed, 3 insertions(+), 3 deletions(-)
    Creating tag '0.0.2'...
    The following commands will be executed to push the changes and tag to the remote repository:
      /usr/bin/git push origin master
      /usr/bin/git push --tags
    Execute commands to push the local commits and tags to the remote repository [Y/n]?
    Username for 'https://github.com': lucasw
    Password for 'https://lucasw@github.com':
    Counting objects: 8, done.
    Delta compression using up to 8 threads.
    Compressing objects: 100% (4/4), done.
    Writing objects: 100% (4/4), 392 bytes | 0 bytes/s, done.
    Total 4 (delta 3), reused 0 (delta 0)
    To https://github.com/lucasw/screen_grab.git
       ceed766..69c167d  master -> master
    Username for 'https://github.com': lucasw
    Password for 'https://lucasw@github.com':
    Total 0 (delta 0), reused 0 (delta 0)
    To https://github.com/lucasw/screen_grab.git
     * [new tag]         0.0.2 -> 0.0.2
    The source repository has been released successfully. The next step will be 'bloom-release'.

