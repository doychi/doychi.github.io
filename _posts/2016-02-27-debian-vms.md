---
layout: post
title:  "Debian VMs"
date:   2016-02-27 21:03
categories: debian virutal server configuration
---

**This is an unfinished with updates to come**

Well, when I was shutting down my PC last week Windows crashed and apparently corrupted my development VM.  A very sad situation, as I didn't have backups of the virutal machine disks.  Fortunately the only thing I have really lost is the configuration, which is largely documented in this blog, but there are some missing bits.

This entry documents my setup for Debian this time round.  Of course I will be referencing my previous posts, where appropraite.

## References
[vbox]: https://www.virtualbox.org/ "VirtualBox"
[hv]: https://msdn.microsoft.com/en-us/virtualization/hyperv_on_windows/windows_welcome?f=255&MSPPError=-2147217396 "Hyper-V"
[deb]: https://www.debian.org/ "Debian"
[osb]: http://www.osboxes.org/debian-8-jessie-images-available-for-virtualbox-and-vmware/ "Debian 8 from OSBoxes"
[git]: https://git-scm.com/ "Git distributed version control system"
[i3]: http://i3wm.org/ "i3 tiling window manager"
[vim]: http://www.vim.org/" "VIm - Vi Improved"
[dots]: https://github.com/EvanPurkhiser/dots/blob/master/README.md "Dots - A dotfile Management Tool"

1. [Debian][deb]
2. [Hyper-V][hv]
3. [Git][git]
4. [i3 Tiling Window Manager][i3]
3. [Osboxes][osb]
4. [Vim][vim]
3. [VirtualBox][vbox]

## Overview

So at home I run Windows 10 for my desktop OS so that I can play games without any trouble.  This setup would allow me to run [Hyper-V][hv], but that would mean that the I couldn't transfer the VM to my MacBoo Pro (not that I have yet), so I have setup [VirtualBox][vbox] instead.

In rebuilding the VM this time round I decided not to install [Debian][deb] from scratch.  I  hear a bunch of you asking why.  Well the answer is that I thought it would take longer.  I'm not sure whether I was right or not, but it seems to be working so far (I started writing this blog after getting most the way through the rebuild, so be warned).

A quick Google search found me the latest Debian (8 a.k.a. Jessie) build as a 64bit VirtualBox VM from [OSBoxes][osb].  So the rest of the process is about updating or modifying this image to be my own.

The rest of this entry is my best attempt to recreate the steps I took to update the OSBoxes version of Debian.  It should be enough to allow me to rebuild a VM again if I need to.

### Setup

The key components of my setup are:

* [Debian][deb]
* [i3][i3] Window Manager
* [dots][dots]
* [Vim][vim]
* [Git][git]


## Basic Steps

1. Install the VM in VirtualBox
2. Remove unwanted packages
3. Install key packages, e.g. Vim and Git
3. Apply the dots configuration
4. Clone my repos for development

## Install the VM in VirtualBox

## Remove Unwanted Packages

{% highlight bash %}
aptitude purge libreoffice
dpkg -l|grep libreoffice|awk '{print $2}'|xargs aptitude purge
aptitude purge apache2
aptitude purge apache2-bin libapache2-mod-dnssd
aptitude purge gdm3 task-gnome-desktop gnome-shell metacity mutter
aptitude purge gnome-terminal gnome-terminal-data
{% endhighlight %}

## Install Key Packages

{% highlight bash %}
aptitude install vim i3 netselect-apt slim
aptitude install xdg-utils xdg-user-dirs
aptitude install dpkg-buildpackage
aptitude install dh_make git-buildpackage
aptitude install dh-make git-buildpackage
aptitude install rxvt-unicode-256color
aptitude install dh-make git-buildpackage
aptitude install ssh
{% endhighlight %}

## Apply the dots Configuration

## Clone My Repos for Development
