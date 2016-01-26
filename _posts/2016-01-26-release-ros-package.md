---
title: Releasing screen_grab ROS package
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

Next bloom release:

    ~/catkin_ws/src/screen_grab$ bloom-release --rosdistro jade --track jade screen_grab --edit
    ROS Distro index file associate with commit 'fc052dc2d908eb765b21a6f7d539ec89835c8c1e'
    New ROS Distro index url: 'https://raw.githubusercontent.com/ros/rosdistro/fc052dc2d908eb765b21a6f7d539ec89835c8c1e/index.yaml'
    Specified repository 'screen_grab' is not in the distribution file located at 'https://raw.githubusercontent.com/ros/rosdistro/fc052dc2d908eb765b21a6f7d539ec89835c8c1e/jade/distribution.yaml'
    Could not determine release repository url for repository 'screen_grab' of distro 'jade'
    You can continue the release process by manually specifying the location of the RELEASE repository.
    To be clear this is the url of the RELEASE repository not the upstream repository.
    For release repositories on GitHub, you should provide the `https://` url which should end in `.git`.
    Here is the url for a typical release repository on GitHub: https://github.com/ros-gbp/rviz-release.git
    ==> Looking for a release of this repository in a different distribution...
    No reasonable default release repository url could be determined from previous releases.
    Release repository url [press enter to abort]: https://github.com/lucasw/screen_grab-release.git
    ==> Fetching 'screen_grab' repository from 'https://github.com/lucasw/screen_grab-release.git'
    Cloning into '/tmp/tmpqTbvP2'...
    remote: Counting objects: 3, done.
    remote: Compressing objects: 100% (2/2), done.
    remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
    Unpacking objects: 100% (3/3), done.
    Checking connectivity... done.
    Creating track 'jade'...
    Repository Name:
      upstream
        Default value, leave this as upstream if you are unsure
      <name>
        Name of the repository (used in the archive name)
      ['upstream']: 
    Upstream Repository URI:
      <uri>
        Any valid URI. This variable can be templated, for example an svn url
        can be templated as such: "https://svn.foo.com/foo/tags/foo-:{version}"
        where the :{version} token will be replaced with the version for this release.
      [None]: https://github.com/lucasw/screen_grab.git
    Upstream VCS Type:
      svn
        Upstream URI is a svn repository
      git
        Upstream URI is a git repository
      hg
        Upstream URI is a hg repository
      tar
        Upstream URI is a tarball
      ['git']: 
    Version:
      :{ask}
        This means that the user will be prompted for the version each release.
        This also means that the upstream devel will be ignored.
      :{auto}
        This means the version will be guessed from the devel branch.
        This means that the devel branch must be set, the devel branch must exist,
        and there must be a valid package.xml in the upstream devel branch.
      <version>
        This will be the version used.
        It must be updated for each new upstream version.
      [':{auto}']: 
    Release Tag:
      :{none}
        For svn and tar only you can set the release tag to :{none}, so that
        it is ignored.  For svn this means no revision number is used.
      :{ask}
        This means the user will be prompted for the release tag on each release.
      :{version}
        This means that the release tag will match the :{version} tag.
        This can be further templated, for example: "foo-:{version}" or "v:{version}"
        
        This can describe any vcs reference. For git that means {tag, branch, hash},
        for hg that means {tag, branch, hash}, for svn that means a revision number.
        For tar this value doubles as the sub directory (if the repository is
        in foo/ of the tar ball, putting foo here will cause the contents of
        foo/ to be imported to upstream instead of foo itself).
      [':{version}']: 
    Upstream Devel Branch:
      <vcs reference>
        Branch in upstream repository on which to search for the version.
        This is used only when version is set to ':{auto}'.
      [None]: master
    ROS Distro:
      <ROS distro>
        This can be any valid ROS distro, e.g. groovy, hydro
      ['jade']: jade
    Patches Directory:
      :{none}
        Use this if you want to disable overlaying of files.
      <path in bloom branch>
        This can be any valid relative path in the bloom branch. The contents
        of this folder will be overlaid onto the upstream branch after each
        import-upstream.  Additionally, any package.xml files found in the
        overlay will have the :{version} string replaced with the current
        version being released.
      [None]: 
    Release Repository Push URL:
      :{none}
        This indicates that the default release url should be used.
      <url>
        (optional) Used when pushing to remote release repositories. This is only
        needed when the release uri which is in the rosdistro file is not writable.
        This is useful, for example, when a releaser would like to use a ssh url
        to push rather than a https:// url.
      [None]: 
    Created 'jade' track.
    ==> Testing for push permission on release repository
    ==> git remote -v
    origin  https://github.com/lucasw/screen_grab-release.git (fetch)
    origin  https://github.com/lucasw/screen_grab-release.git (push)
    ==> git push --dry-run
    Username for 'https://github.com': lucasw
    Password for 'https://lucasw@github.com': 
    To https://github.com/lucasw/screen_grab-release.git
       61fdf59..fdd25a2  master -> master
    ==> Releasing 'screen_grab' using release track 'jade'
    ==> git-bloom-release jade
    Processing release track settings for 'jade'
    Checking upstream devel branch for package.xml(s)
    Cloning into '/tmp/tmpwMkuvL/upstream'...
    remote: Counting objects: 164, done.
    remote: Compressing objects: 100% (53/53), done.
    remote: Total 164 (delta 10), reused 0 (delta 0), pack-reused 108
    Receiving objects: 100% (164/164), 34.13 KiB | 0 bytes/s, done.
    Resolving deltas: 100% (72/72), done.
    Checking connectivity... done.
    Looking for packages in 'master' branch... found 'screen_grab'.
    Detected version '0.0.2' from package(s): ['screen_grab']

    Executing release track 'jade'
    ==> bloom-export-upstream /tmp/tmpwMkuvL/upstream git --tag 0.0.2 --display-uri https://github.com/lucasw/screen_grab.git --name upstream --output-dir /tmp/tmpOBxYoY
    Checking out repository at 'https://github.com/lucasw/screen_grab.git' to reference '0.0.2'.
    Exporting to archive: '/tmp/tmpOBxYoY/upstream-0.0.2.tar.gz'
    md5: 99ae8cebff02761ac0dbaa80cbb4021d

    ==> git-bloom-import-upstream /tmp/tmpOBxYoY/upstream-0.0.2.tar.gz  --release-version 0.0.2 --replace
    Creating upstream branch.
    Importing archive into upstream branch...
    Creating tag: 'upstream/0.0.2'
    I'm happy.  You should be too.

    ==> git-bloom-generate -y rosrelease jade --source upstream -i 0
    Releasing package: ['screen_grab']
    Releasing package 'screen_grab' for 'jade' to: 'release/jade/screen_grab'

    ==> git-bloom-generate -y rosdebian --prefix release/jade jade -i 0
    Generating source debs for the packages: ['screen_grab']
    Debian Incremental Version: 0
    Debian Distributions: ['trusty', 'utopic', 'vivid']
    Releasing for rosdistro: jade

    Pre-verifying Debian dependency keys...
    Running 'rosdep update'...
    All keys are OK

    Placing debian template files into 'debian/jade/screen_grab' branch.
    ==> Placing templates files in the 'debian' folder.

    ####
    #### Generating 'trusty' debian for package 'screen_grab' at version '0.0.2-0'
    ####
    Generating debian for trusty...
    No historical releaser history, using current maintainer name and email for each versioned changelog entry.
    Package 'screen-grab' has dependencies:
    Run Dependencies:
      rosdep key           => trusty key
      dynamic_reconfigure  => ['ros-jade-dynamic-reconfigure']
      nodelet              => ['ros-jade-nodelet']
      roscpp               => ['ros-jade-roscpp']
      sensor_msgs          => ['ros-jade-sensor-msgs']
      std_msgs             => ['ros-jade-std-msgs']
    Build and Build Tool Dependencies:
      rosdep key           => trusty key
      cv_bridge            => ['ros-jade-cv-bridge']
      dynamic_reconfigure  => ['ros-jade-dynamic-reconfigure']
      image_transport      => ['ros-jade-image-transport']
      nodelet              => ['ros-jade-nodelet']
      roscpp               => ['ros-jade-roscpp']
      roslint              => ['ros-jade-roslint']
      sensor_msgs          => ['ros-jade-sensor-msgs']
      std_msgs             => ['ros-jade-std-msgs']
      catkin               => ['ros-jade-catkin']
    ==> In place processing templates in 'debian' folder.
    Expanding 'debian/control.em' -> 'debian/control'
    Expanding 'debian/changelog.em' -> 'debian/changelog'
    Expanding 'debian/gbp.conf.em' -> 'debian/gbp.conf'
    Expanding 'debian/rules.em' -> 'debian/rules'
    Expanding 'debian/compat.em' -> 'debian/compat'
    Creating tag: debian/ros-jade-screen-grab_0.0.2-0_trusty
    ####
    #### Successfully generated 'trusty' debian for package 'screen_grab' at version '0.0.2-0'
    ####


    ####
    #### Generating 'utopic' debian for package 'screen_grab' at version '0.0.2-0'
    ####
    Generating debian for utopic...
    No historical releaser history, using current maintainer name and email for each versioned changelog entry.
    Package 'screen-grab' has dependencies:
    Run Dependencies:
      rosdep key           => utopic key
      dynamic_reconfigure  => ['ros-jade-dynamic-reconfigure']
      nodelet              => ['ros-jade-nodelet']
      roscpp               => ['ros-jade-roscpp']
      sensor_msgs          => ['ros-jade-sensor-msgs']
      std_msgs             => ['ros-jade-std-msgs']
    Build and Build Tool Dependencies:
      rosdep key           => utopic key
      cv_bridge            => ['ros-jade-cv-bridge']
      dynamic_reconfigure  => ['ros-jade-dynamic-reconfigure']
      image_transport      => ['ros-jade-image-transport']
      nodelet              => ['ros-jade-nodelet']
      roscpp               => ['ros-jade-roscpp']
      roslint              => ['ros-jade-roslint']
      sensor_msgs          => ['ros-jade-sensor-msgs']
      std_msgs             => ['ros-jade-std-msgs']
      catkin               => ['ros-jade-catkin']
    ==> In place processing templates in 'debian' folder.
    Expanding 'debian/control.em' -> 'debian/control'
    Expanding 'debian/changelog.em' -> 'debian/changelog'
    Expanding 'debian/gbp.conf.em' -> 'debian/gbp.conf'
    Expanding 'debian/rules.em' -> 'debian/rules'
    Expanding 'debian/compat.em' -> 'debian/compat'
    Creating tag: debian/ros-jade-screen-grab_0.0.2-0_utopic
    ####
    #### Successfully generated 'utopic' debian for package 'screen_grab' at version '0.0.2-0'
    ####


    ####
    #### Generating 'vivid' debian for package 'screen_grab' at version '0.0.2-0'
    ####
    Generating debian for vivid...
    No historical releaser history, using current maintainer name and email for each versioned changelog entry.
    Package 'screen-grab' has dependencies:
    Run Dependencies:
      rosdep key           => vivid key
      dynamic_reconfigure  => ['ros-jade-dynamic-reconfigure']
      nodelet              => ['ros-jade-nodelet']
      roscpp               => ['ros-jade-roscpp']
      sensor_msgs          => ['ros-jade-sensor-msgs']
      std_msgs             => ['ros-jade-std-msgs']
    Build and Build Tool Dependencies:
      rosdep key           => vivid key
      cv_bridge            => ['ros-jade-cv-bridge']
      dynamic_reconfigure  => ['ros-jade-dynamic-reconfigure']
      image_transport      => ['ros-jade-image-transport']
      nodelet              => ['ros-jade-nodelet']
      roscpp               => ['ros-jade-roscpp']
      roslint              => ['ros-jade-roslint']
      sensor_msgs          => ['ros-jade-sensor-msgs']
      std_msgs             => ['ros-jade-std-msgs']
      catkin               => ['ros-jade-catkin']
    ==> In place processing templates in 'debian' folder.
    Expanding 'debian/control.em' -> 'debian/control'
    Expanding 'debian/changelog.em' -> 'debian/changelog'
    Expanding 'debian/gbp.conf.em' -> 'debian/gbp.conf'
    Expanding 'debian/rules.em' -> 'debian/rules'
    Expanding 'debian/compat.em' -> 'debian/compat'
    Creating tag: debian/ros-jade-screen-grab_0.0.2-0_vivid
    ####
    #### Successfully generated 'vivid' debian for package 'screen_grab' at version '0.0.2-0'
    ####


    ==> git-bloom-generate -y rosrpm --prefix release/jade jade -i 0
    Generating source RPMs for the packages: ['screen_grab']
    RPM Incremental Version: 0
    RPM Distributions: ['21', '22']
    Releasing for rosdistro: jade

    Pre-verifying RPM dependency keys...
    Running 'rosdep update'...
    All keys are OK

    Placing RPM template files into 'rpm/jade/screen_grab' branch.
    ==> Placing templates files in the 'rpm' folder.

    ####
    #### Generating '21' RPM for package 'screen_grab' at version '0.0.2-0'
    ####
    Generating RPM for 21...
    Package 'screen-grab' has dependencies:
    Run Dependencies:
      rosdep key           => 21 key
      dynamic_reconfigure  => ['ros-jade-dynamic-reconfigure']
      nodelet              => ['ros-jade-nodelet']
      roscpp               => ['ros-jade-roscpp']
      sensor_msgs          => ['ros-jade-sensor-msgs']
      std_msgs             => ['ros-jade-std-msgs']
    Build and Build Tool Dependencies:
      rosdep key           => 21 key
      cv_bridge            => ['ros-jade-cv-bridge']
      dynamic_reconfigure  => ['ros-jade-dynamic-reconfigure']
      image_transport      => ['ros-jade-image-transport']
      nodelet              => ['ros-jade-nodelet']
      roscpp               => ['ros-jade-roscpp']
      roslint              => ['ros-jade-roslint']
      sensor_msgs          => ['ros-jade-sensor-msgs']
      std_msgs             => ['ros-jade-std-msgs']
      catkin               => ['ros-jade-catkin']
    ==> In place processing templates in 'rpm' folder.
    Expanding 'rpm/template.spec.em' -> 'rpm/template.spec'
    Creating tag: rpm/ros-jade-screen-grab-0.0.2-0_21
    ####
    #### Successfully generated '21' RPM for package 'screen_grab' at version '0.0.2-0'
    ####


    ####
    #### Generating '22' RPM for package 'screen_grab' at version '0.0.2-0'
    ####
    Generating RPM for 22...
    Package 'screen-grab' has dependencies:
    Run Dependencies:
      rosdep key           => 22 key
      dynamic_reconfigure  => ['ros-jade-dynamic-reconfigure']
      nodelet              => ['ros-jade-nodelet']
      roscpp               => ['ros-jade-roscpp']
      sensor_msgs          => ['ros-jade-sensor-msgs']
      std_msgs             => ['ros-jade-std-msgs']
    Build and Build Tool Dependencies:
      rosdep key           => 22 key
      cv_bridge            => ['ros-jade-cv-bridge']
      dynamic_reconfigure  => ['ros-jade-dynamic-reconfigure']
      image_transport      => ['ros-jade-image-transport']
      nodelet              => ['ros-jade-nodelet']
      roscpp               => ['ros-jade-roscpp']
      roslint              => ['ros-jade-roslint']
      sensor_msgs          => ['ros-jade-sensor-msgs']
      std_msgs             => ['ros-jade-std-msgs']
      catkin               => ['ros-jade-catkin']
    ==> In place processing templates in 'rpm' folder.
    Expanding 'rpm/template.spec.em' -> 'rpm/template.spec'
    Creating tag: rpm/ros-jade-screen-grab-0.0.2-0_22
    ####
    #### Successfully generated '22' RPM for package 'screen_grab' at version '0.0.2-0'
    ####





    Tip: Check to ensure that the debian tags created have the same version as the upstream version you are releasing.
    Everything went as expected, you should check that the new tags match your expectations, and then push to the release repo with:
      git push --all && git push --tags  # You might have to add --force to the second command if you are over-writing existing tags
    <== Released 'screen_grab' using release track 'jade' successfully
    ==> git remote -v
    origin  https://github.com/lucasw/screen_grab-release.git (fetch)
    origin  https://github.com/lucasw/screen_grab-release.git (push)
    Releasing complete, push to release repository?
    Continue [Y/n]? 
    ==> Pushing changes to release repository for 'screen_grab'
    ==> git push --all
    Username for 'https://github.com': lucasw
    Password for 'https://lucasw@github.com': 
    Counting objects: 181, done.
    Delta compression using up to 8 threads.
    Compressing objects: 100% (157/157), done.
    Writing objects: 100% (179/179), 30.92 KiB | 0 bytes/s, done.
    Total 179 (delta 41), reused 0 (delta 0)
    To https://github.com/lucasw/screen_grab-release.git
       61fdf59..f0e1973  master -> master
     * [new branch]      debian/jade/screen_grab -> debian/jade/screen_grab
     * [new branch]      debian/jade/trusty/screen_grab -> debian/jade/trusty/screen_grab
     * [new branch]      debian/jade/utopic/screen_grab -> debian/jade/utopic/screen_grab
     * [new branch]      debian/jade/vivid/screen_grab -> debian/jade/vivid/screen_grab
     * [new branch]      patches/debian/jade/screen_grab -> patches/debian/jade/screen_grab
     * [new branch]      patches/debian/jade/trusty/screen_grab -> patches/debian/jade/trusty/screen_grab
     * [new branch]      patches/debian/jade/utopic/screen_grab -> patches/debian/jade/utopic/screen_grab
     * [new branch]      patches/debian/jade/vivid/screen_grab -> patches/debian/jade/vivid/screen_grab
     * [new branch]      patches/release/jade/screen_grab -> patches/release/jade/screen_grab
     * [new branch]      patches/rpm/jade/21/screen_grab -> patches/rpm/jade/21/screen_grab
     * [new branch]      patches/rpm/jade/22/screen_grab -> patches/rpm/jade/22/screen_grab
     * [new branch]      patches/rpm/jade/screen_grab -> patches/rpm/jade/screen_grab
     * [new branch]      release/jade/screen_grab -> release/jade/screen_grab
     * [new branch]      rpm/jade/21/screen_grab -> rpm/jade/21/screen_grab
     * [new branch]      rpm/jade/22/screen_grab -> rpm/jade/22/screen_grab
     * [new branch]      rpm/jade/screen_grab -> rpm/jade/screen_grab
     * [new branch]      upstream -> upstream
    <== Pushed changes successfully
    ==> Pushing tags to release repository for 'screen_grab'
    ==> git push --tags
    Username for 'https://github.com': lucasw
    Password for 'https://lucasw@github.com': 
    Total 0 (delta 0), reused 0 (delta 0)
    To https://github.com/lucasw/screen_grab-release.git
     * [new tag]         debian/ros-jade-screen-grab_0.0.2-0_trusty -> debian/ros-jade-screen-grab_0.0.2-0_trusty
     * [new tag]         debian/ros-jade-screen-grab_0.0.2-0_utopic -> debian/ros-jade-screen-grab_0.0.2-0_utopic
     * [new tag]         debian/ros-jade-screen-grab_0.0.2-0_vivid -> debian/ros-jade-screen-grab_0.0.2-0_vivid
     * [new tag]         release/jade/screen_grab/0.0.2-0 -> release/jade/screen_grab/0.0.2-0
     * [new tag]         rpm/ros-jade-screen-grab-0.0.2-0_21 -> rpm/ros-jade-screen-grab-0.0.2-0_21
     * [new tag]         rpm/ros-jade-screen-grab-0.0.2-0_22 -> rpm/ros-jade-screen-grab-0.0.2-0_22
     * [new tag]         upstream/0.0.2 -> upstream/0.0.2
    <== Pushed tags successfully
    ==> Generating pull request to distro file located at 'https://raw.githubusercontent.com/ros/rosdistro/fc052dc2d908eb765b21a6f7d539ec89835c8c1e/jade/distribution.yaml'
    Would you like to add documentation information for this repository? [Y/n]? 
    ==> Looking for a doc entry for this repository in a different distribution...
    No existing doc entries found for use as defaults.
    Please enter your repository information for the doc generation job.
    This information should point to the repository from which documentation should be generated.
    VCS Type must be one of git, svn, hg, or bzr.
    VCS type: git
    VCS url: https://github.com/lucasw/screen_grab.git
    VCS version must be a branch, tag, or commit, e.g. master or 0.1.0
    VCS version: 0.0.2
    Would you like to add source information for this repository? [Y/n]? 
    ==> Looking for a source entry for this repository in a different distribution...
    No existing source entries found for use as defaults.
    Please enter information which points to the active development branch for this repository.
    This information is used to run continuous integration jobs and for developers to checkout from.
    VCS Type must be one of git, svn, hg, or bzr.
    VCS type: https://github.com/lucasw/screen_grab.git
    'https://github.com/lucasw/screen_grab.git' is not a valid vcs type.
    Try again [Y/n]? 
    VCS Type must be one of git, svn, hg, or bzr.
    VCS type: git
    VCS url: https://github.com/lucasw/screen_grab.git
    VCS version must be a branch, tag, or commit, e.g. master or 0.1.0
    VCS version: master
    Would you like to add a maintenance status for this repository? [Y/n]? 
    Please enter a maintenance status.
    Valid maintenance statuses:
    - developed: active development is in progress
    - maintained: no new development, but bug fixes and pull requests are addressed
    - end-of-life: should not be used, will disappear at some point
    Status: developed
    You can also enter a status description.
    This is usually reserved for giving a reason when a status is 'end-of-life'.
    Status Description [press Enter for no change]: 
    Unified diff for the ROS distro file located at '/tmp/tmpzV70RA/screen_grab-0.0.2-0.patch':
    --- fc052dc2d908eb765b21a6f7d539ec89835c8c1e/jade/distribution.yaml
    +++ fc052dc2d908eb765b21a6f7d539ec89835c8c1e/jade/distribution.yaml
    @@ -4773,6 +4773,21 @@
           url: https://github.com/SmartRoboticSystems/schunk_grippers.git
           version: master
         status: maintained
    +  screen_grab:
    +    doc:
    +      type: git
    +      url: https://github.com/lucasw/screen_grab.git
    +      version: 0.0.2
    +    release:
    +      tags:
    +        release: release/jade/{package}/{version}
    +      url: https://github.com/lucasw/screen_grab-release.git
    +      version: 0.0.2-0
    +    source:
    +      type: git
    +      url: https://github.com/lucasw/screen_grab.git
    +      version: master
    +    status: developed
       serial:
         doc:
           type: git

    Looks like bloom doesn't have an oauth token for you yet.
    Therefore bloom will require your GitHub username and password just this once.
    With your GitHub username and password bloom will create an oauth token on your behalf.
    The token will be stored in `~/.config/bloom`.
    You can delete the token from that file to have a new token generated.
    Guard this token like a password, because it allows someone/something to act on your behalf.
    If you need to unauthorize it, remove it from the 'Applications' menu in your GitHub account page.

    Would you like to create an OAuth token now [Y/n]? 
    GitHub username [lucasw]: lucasw
    GitHub password (never stored): 
    The token 'foo' was created and stored in the bloom config file: '/home/lucasw/.config/bloom'
    ==> Checking on GitHub for a fork to make the pull request from...
    ==> lucasw/rosdistro is not a fork, searching...
    Could not find a fork of ros/rosdistro on the lucasw GitHub account.
    Would you like to create one now?
    Continue [Y/n]? 
    ==> Using this fork to make a pull request from: lucasw/rosdistro
    ==> Cloning lucasw/rosdistro...
    ==> mkdir -p rosdistro
    ==> git init
    Initialized empty Git repository in /tmp/55qIfn/rosdistro/.git/
    Pull Request Title: screen_grab: 0.0.2-0 in 'jade/distribution.yaml' [bloom]
    Pull Request Body : 
    Increasing version of package(s) in repository `screen_grab` to `0.0.2-0`:

    - upstream repository: https://github.com/lucasw/screen_grab.git
    - release repository: https://github.com/lucasw/screen_grab-release.git
    - distro file: `jade/distribution.yaml`
    - bloom version: `0.5.20`
    - previous version for package: `null`

    ## screen_grab

    - No changes

    Open a pull request from 'rosdistro/rosdistro:bloom-screen_grab-0' into 'ros/rosdistro:master'?
    Continue [Y/n]? 
    ==> git checkout -b bloom-screen_grab-0
    Switched to a new branch 'bloom-screen_grab-0'
    ==> Pulling latest rosdistro branch
    remote: Counting objects: 72092, done.
    remote: Compressing objects: 100% (10/10), done.
    remote: Total 72092 (delta 3), reused 0 (delta 0), pack-reused 72082
    Receiving objects: 100% (72092/72092), 21.53 MiB | 4.95 MiB/s, done.
    Resolving deltas: 100% (45608/45608), done.
    From https://github.com/ros/rosdistro
     * branch            master     -> FETCH_HEAD
    ==> git reset --hard fc052dc2d908eb765b21a6f7d539ec89835c8c1e
    HEAD is now at fc052dc Merge pull request #10355 from 130s/bloom-force_torque_tools-0
    ==> Writing new distribution file: jade/distribution.yaml
    ==> git add jade/distribution.yaml
    ==> git commit -m "screen_grab: 0.0.2-0 in 'jade/distribution.yaml' [bloom]"
    [bloom-screen_grab-0 4216d50] screen_grab: 0.0.2-0 in 'jade/distribution.yaml' [bloom]
     1 file changed, 15 insertions(+)
    ==> Pushing changes to fork
    Counting objects: 7, done.
    Delta compression using up to 8 threads.
    Compressing objects: 100% (4/4), done.
    Writing objects: 100% (4/4), 446 bytes | 0 bytes/s, done.
    Total 4 (delta 3), reused 0 (delta 0)
    To https://foo:x-oauth-basic@github.com/lucasw/rosdistro.git
     * [new branch]      bloom-screen_grab-0 -> bloom-screen_grab-0
    <== Pull request opened at: https://github.com/ros/rosdistro/pull/10356

