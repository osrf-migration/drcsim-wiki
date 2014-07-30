How to prepare a laptop for use at the DRC Kickoff
=

This page explains how to prepare a laptop for use at the DRC Simulator tutorial, which is happening in Washington, DC on Oct 25, 2012, as part of the DRC Kickoff meeting that week.  These instructions are intended specifically for preparing the Dell Latitude E6420 laptops that will be provided at the tutorial.

## Update Laptop BIOS ##

On boot, press F12 to go into the system BIOS.  Expand the "video" tab in the left side panel, and check to see that the "Optimus" option is enabled.

## Install Ubuntu Linux ##

Perform a standard installation of Ubuntu 12.04 (precise).

1. Prepare a Ubuntu 12.04 (precise) 64-bit installation USB stick.  Find instructions for that somewhere.
1. Boot the computer with the USB stick inserted.  When prompted, press F12 to get to BIOS configuration.
1. Select the option to boot from the USB storage device.
1. Use the GUI to install the default system, using the entire hard drive.
  1. Do select "Download updates while installing" but do '''not''' select "Install this third-party software"
  1. Create a user 'drcsim' with some obvious password and enable auto-login for that user.
  1. Set the timezone to Eastern.
1. Reboot.

## Turn off update checking ##

1. Don't install updates.
1. Open the Update Manager, click Settings...->Updates->Automatically check for updates: Never.

## Switch to simpler session ##

1. Install gnome-session-fallback:

        sudo apt-get install -y gnome-session-fallback

1. Log out.

1. Select session "GNOME Classic (No effects)" and login.

## Add applications to the dock ##

1. Drag Terminal (Applications->Accessories->Terminal) to the top dock.
1. Drag Firefox (Applications->Internet->Firefox Web Browser) to the top dock.

## Upgrade the kernel ##

The graphics hardware in the E6240 is problematic under the 3.2 kernel provided with Ubuntu 12.04.  Manually upgade to the 3.4.0 kernel.

1. Install dkms (TODO: verify that this step is necessary):

        sudo apt-get install -y dkms

1. Download 3.4.0 kernel packages:

        wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v3.4-precise/linux-headers-3.4.0-030400-generic_3.4.0-030400.201205210521_amd64.deb
        wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v3.4-precise/linux-headers-3.4.0-030400_3.4.0-030400.201205210521_all.deb
        wget http://kernel.ubuntu.com/~kernel-ppa/mainline/v3.4-precise/linux-image-3.4.0-030400-generic_3.4.0-030400.201205210521_amd64.deb

1. Install the new kernel

        sudo dpkg -i *.deb      

1. Reboot.

## Install DRC Simulator ##

We want to [[InstallDRC|install the DRC Simulator software]], as well as extra software that will be used in the [[Tutorials/drcsim/|tutorials]].  At present, that process is:

        sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu precise main" > /etc/apt/sources.list.d/ros-latest.list'
        sudo sh -c 'echo "deb http://packages.osrfoundation.org/drc/ubuntu precise main" > /etc/apt/sources.list.d/drc-latest.list'
        wget http://packages.ros.org/ros.key -O - | sudo apt-key add -
        wget http://packages.osrfoundation.org/drc.key -O - | sudo apt-key add -
        sudo apt-get update
        sudo apt-get install -y drcsim
        sudo apt-get install -y ros-fuerte-visualization ros-fuerte-pr2-teleop-app
        sudo apt-get install -y build-essential vim emacs nano mercurial gimp blender meshlab cmake-curses-gui vim-gnome meld dirdiff mesa-utils recordmydesktop
        # Setup shell
        echo 'source /usr/share/drcsim-1.1/setup.sh' >> ~/.bashrc
        # Prevent warning dialog from rviz on first execution
        mkdir -p ~/.rviz
        touch ~/.rviz/display_config ~/.rviz/config
        # Clone the online database to avoid the need to download it later.
        mkdir -p ~/.gazebo
        hg clone https://bitbucket.org/osrf/gazebo_models ~/.gazebo/models

## Install other software ##

1. Install flash, needed to watch YouTube videos linked from within the ROS wiki.
  1. Open the Ubuntu Software Center.
  1. Type "flash" without quotes into the search box and hit enter.
  1. Click on Adobe Flash Plugin in the search results.
  1. Click the Install button.
