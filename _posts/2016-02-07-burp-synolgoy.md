---
layout: post
title:  "Burp Backup Configuration for Synology Diskstation"
date:   2016-02-07 12:20:43
categories: backup synology burp
---
**Updated 19 Feb 2016 - Resolved compilation issues**

I've had Burp setup before in my home environment.  I found it to be pretty effective, but now I have a [Synology NAS][syno] and want to move the backups to this device.  In this entry I will be configuring [Burp][burp] on a Synology DS414, using the [SynoCommunity][comm] [Debian][synodeb] environment.

## References 
[burp]: https://burp.grke.org/ "Burp Backup"
[syno]: http://www.synology.com/ "Synology NAS"
[comm]: https://synocommunity.com/ "SynoCommunity"
[dsm]: htts://www.synology.com/en-us/dsm/ "Synology DiskStation Manager"
[synodeb]: https://github.com/SynoCommunity/spksrc/wiki/Debian-Chroot "SynCommunity Debian"

1. [Burp Backup][burp]
1. [Synology][syno]
1. [Synology DSM][dsm]
1. [SynCommunity][comm]
1. [SynoCommunity Debian][synodeb]

## Tasks

1. Install Synology DSM.
1. Install Debian, using the SynoCommunity package.
1. Install Build Tools (to Compile and Install Burp).
1. Install Burp
1. Configure Burp and Burp clients

## Steps

### Install Synolgoy DSM

Installing the Synolgoy DSM is as simple as following the prompts when connecting to the DSM. There is nothing special about the DSM installation and the basic installation is sufficient to get started with Burp.  At the time of writing the manual is available at [User Guide](https://global.download.synology.com/download/Document/UserGuide/DSM/).

### Install Debian

Installing Debian is pretty easy to install and the installation process on the [SynCommunity site][syno] and the [SynoCommunity Debian page][synodeb] is pretty simple.  As an overview, just in case the instructions disappear or move, they are:

1. Modify the allowed package sources, by going to ``Menu -> Package Centre -> Settings``.
1. Set the Trust Level to "Synology Inc. and trusted publishers".
1. Add the SynoCommunity package repository, by going to ``Menu -> Package Centre -> Settings -> Package Sources``.

    1. Enter ``SynoCommunity`` into the Name field.
    1. Enter ``http://packages.synocommunity.com/`` into the Location field
    1. Press Ok.

Everything should now be ready to install Debian, by:

1. Go to ``Menu -> Package Centre -> Community``.
1. Find ``Debian Chroot``.
1. Click "Install".  This will install the Python and Debian Chroot packages.

Once installed, the [SynoCommunity Debian] packages instructions should be followed.  This is broadly:

1. Login to the diskstation via SSH and obtain root access.  On DSM 6 and above, this is not done using the root user as in previous version.  You will need to login using the administrator account set up during the DSM install and using ``sudo`` or ``su``.
1. Start the chroot environment, using the command ``/var/packages/debian-chroot/scripts/start-stop-status chroot``.
1. Update the Debian packages in the chroot environment, using apt-get as aptitude is not installed.
1. Set up the Debian Chroot environment as a service, by going to ``Menu -> Control Panel -> Info Center -> Services``.
1. Find "Debian Chroot" in the list of services and check the "Enable" check box and click "Save".

### Install Build Tools (to Compile and Install Burp)

The build environment for Burp is pretty standard and can be installed with the command:

> apt-get install librsync-dev libz-dev libssl-dev uthash-dev libyajl-dev libncurses5-dev librsync1
make g++ dh-make fakeroot dh-autoreconf libtinfo-dev libattr1-dev libacl1-dev

- dh-make - This package is for building a Burp Debian package
- dh-autoreconf - This package is also for building a Burp Debian package
- fakeroot - This package is the thrid for building a Burp Debian package
- All of the other packages are dependencies for Burp

Follow the dh-make instructions in [How To Build a Package from Source the Smart Way](http://forums.debian.net/viewtopic.php?t=38976).

1. ``wget http://download.sourceforge.net/project/burp/burp-1.4.40/burp-1.4.40.tar.bz2``
1. Extract the file into a directory, as per the link above.
1. Rename the source file ``mv burp-1.4.40.tar.bz2 burp-1.4.40.orig.tar.bz2``
1. Delete the format file:  ``rm debian/source/format``
1. Run the Debian build: ``dpkg-buildpakcage -sa -j3 -us -uc``
