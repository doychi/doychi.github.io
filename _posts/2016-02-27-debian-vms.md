---
layout: post
title:  "Debian VMs"
date:   2016-02-27 21:03 +11:00
updates:
    - date: 2016-03-16 23:45:00 +11:00
      change: Added more detail to the package deletions, the dosts configuration and Jekyll setup for GitHub Pages.
    - date: 2016-03-17 22:31:00 +11:00
      change: Added details about configuring the VM/host interaction.
    - date: 2016-03-18 16:02:00 +11:00
      change: Tidied up the post and added the details about the clipboard setup.
    - date: 2016-04-12 22:32:00 +11:00
      change: Added the change default terminal to URxvt.
    - date: 2016-04-15 13:29:00 +11:00
      change: Added two programs to the list of installs.
    - date: 2016-04-16 00:46:00 +11:00
      change:  Corrected the version of Vim so that the clipboard works with X terminals and corrected the hostname.
    - date: 2017-01-06 22:15 +11:00
      change: Added FZF configuration and replaced The Platinum Searcher with RipGrep.
categories:
    - debian
    - configuration
tags:
    - debian
    - virutal server
    - configuration
---

Well, when I was shutting down my PC last week Windows crashed and apparently
corrupted my development VM.  A very sad situation, as I didn't have backups of
the virutal machine disks.  Fortunately the only thing I have really lost is the
configuration, which is largely documented in this blog, but there are some
missing bits.

This entry documents my setup for Debian this time round.  Of course I will be
referencing my previous posts, where appropraite.

## References
[deb]: https://www.debian.org/ "Debian"
[debreduce]: https://wiki.debian.org/ReduceDebian "Reduce Debian's Install Size"
[dots]: https://github.com/EvanPurkhiser/dots/blob/master/README.md "Dots - A dotfile Management Tool"
[git]: https://git-scm.com/ "Git distributed version control system"
[hv]: https://msdn.microsoft.com/en-us/virtualization/hyperv_on_windows/windows_welcome?f=255&MSPPError=-2147217396 "Hyper-V"
[i3]: http://i3wm.org/ "i3 tiling window manager"
[jitblog]: http://www.jitblog.net/oracle-virtualbox-install-fuest-additions-on-linux/ "JiT Blog"
[osb]: http://www.osboxes.org/debian-8-jessie-images-available-for-virtualbox-and-vmware/ "Debian 8 from OSBoxes"
<!--
[pt]: https://github.com/monochromegane/the_platinum_searchers "The Platinum Searcher"
[pt-rel]: https://github.com/monochromegane/the_platinum_searcher/releases "The Platinum Searcher releases"
-->
[rip]: https://github.com/BurntSushi/ripgrep "RipGrep home page"
[rip-rel]: https://github.com/BurntSushi/ripgrep/releases "RipGrep Release"
[vbox]: https://www.virtualbox.org/ "VirtualBox"
[vim]: http://www.vim.org/" "VIm - Vi Improved"
[vimxclip]: http://www.electricmonk.nl/log/2011/04/05/vim-x11-and-the-clipboard-copy-paste/ "Vim, X11 and the clipboard (Copy, paste)"
[xclip]: https://mutelight.org/subtleties-of-the-x-clipboard "Subtleties of the X Clipboard"
[host]: http://www.cyberciti.biz/faq/debian-change-hostname-permanently/ "nixCraft"
[fzf]: http://github.com/junegunn/fzf "fzf"
[jddots]: {% post_url 2015-05-31-debian-dotfiles %} "Doychi's Dots configuration"

1. [Debian][deb]
1. [fzf][fzf]
1. [Git][git]
1. [Hyper-V][hv]
1. [i3 Tiling Window Manager][i3]
1. [JiT Blog][jitblog]
1. [Osboxes][osb]
1. [Subtleties of the X Clipboard][xclip]
1. [Vim, X11 and the clipboard (Copy, paste)][vimxclip]
1. [Vim][vim]
1. [VirtualBox][vbox]

## Overview

So at home I run Windows 10 for my desktop OS so that I can play games without
any trouble.  This setup could be achieved with to run [Hyper-V][hv], but that
would mean that the I couldn't transfer the VM to my MacBook Pro (not that I
have yet), so I have setup [VirtualBox][vbox] instead.

In rebuilding the VM this time round I decided not to install [Debian][deb] from
scratch.  I  hear a bunch of you asking why.  Well the answer is that I thought
it would take longer.  I'm not sure whether I was right or not, but it seems to
be working so far (I started writing this blog after getting most the way
through the rebuild, so be warned).

A quick Google search found me the latest Debian (8 a.k.a. Jessie) build as a
64bit VirtualBox VM from [OSBoxes][osb].  So the rest of the process is about
updating or modifying this image to be my own.

The rest of this entry is my best attempt to recreate the steps I took to update
the OSBoxes version of Debian.  It should be enough to allow me to rebuild a VM
again if I need to.

### Environment Elements

This configuration is purely the setup of Debian for my development proposes.
This includes the tools/software below, which forms the basis for all my
development.

* [VirutalBox][vbox]
* [Debian][deb]
* [i3][i3] Window Manager
* [dots][dots]
* [Vim][vim]
* [Git][git]
* Other tools, such as [fzf][fzf].


## Installation/Configuration Steps

### High Level Steps

1. Install the VM in VirtualBox
2. Remove unwanted packages
3. Package Installtion
3. Apply the dots configuration
4. Clone my repos for development
5. Install other tools.

### Install the VM in VirtualBox

_NB:  VirtualBox installation is not covered in this post_

1. Follow the installation process for importing a [VirtualBox
   appliance](https://www.virtualbox.org/manual/ch01.html#ovf).
1. Login to the VM and set your correct timezone and locale, by running the
   following commands:

~~~ bash
    $ sudo dpkg-reconfigure locales
    $ sudo dpkg-reconfigure tzdate
~~~

### Remove Necessary Packages

Because the OSBoxes' VM is a general desktop installation and I want a cut down
i3 window manager installation, a number of packages need to be removed.  This
step removes most of these packages.

The following are some links which you may find useful if you want to workout
which packages you want to remove for your enviornment.

* [Debian Cleanup Tip #6: Remove automatically installed packages that are no longer needed](https://raphaelhertzog.com/2011/03/07/debian-cleanup-tip-6-remove-automatically-installed-packages/)
* [Removing unnecessary packages with deborphan](https://www.debian-administration.org/article/134/Removing_unnecessary_packages_with_deborphan)
* [Reducing the size of the Debian Installation Footprint](https://wiki.debian.org/ReduceDebian)
* [Finding packages for deinstallation](http://www.vitavonni.de/blog/201103/2011031502-finding-packages-for-deinstallation.html) - `aptitude search '!?reverse-depends(~i) ~M !?essential'`

But before any packages can be removed, a few packages need to be added to make
life easier.  These packages are:

* deborphan
* ssh
* vim

This is done by running:

~~~ bash
    $ aptitude install ssh vim-gtk deborphan
    $ aptitude purge vim-tiny
~~~

The packages that I removed is covered by the commands below.  Essentially, this
list is anything server based or for Gnome.  I removed the server stuff, because
I don't want to have servers installed when I am not using them (e.g. Apache
HTTPD server).  I remove the Gnome packages because I don't use Gnome to avoid
some performance overhead and I find the i3 window manager very effective for my
software development.

~~~ bash
    $ aptitude purge libreoffice
    $ dpkg -l | grep libreoffice | awk '{print $2}' | xargs aptitude purge -y
    $ aptitude purge gdm3 task-gnome-desktop gnome-shell metacity mutter \
      gnome-terminal gnome-terminal-data apache2 apache2-bin \
      libapache2-mod-dnssd gnome-control-center gnome-user-share
    $ dpkg -l | grep -i gnome | awk '{print $2}' | xargs apt-mark markauto
    $ aptitude purge bogofilter bluez evolution task-laptop evolution-common \
      libreoffice libreoffice-evolution evolution-plugins caribou
      caribou-antler cdrdao cheese cheese-common libcheese-gtk23 libcheese7 \
      coinor-libcbc3 coinor-libcoinmp1 libreoffice unoconv libreoffice-calc
    $ dpkg -l | grep -i burning | awk '{print $2}' | xargs aptitude purge -y
    $ dpkg -l | grep -i coinor | awk '{print $2}' | xargs aptitude purge -y
    $ dpkg -l | grep -i "^..  gnome" | awk '{print $2}' | xargs aptitude purge -y
    $ aptitude purge gedit-common libpam-gnome-keyring gvfs-backends inkscape  \
      nautilus nautilus-data rhythmbox-data totem-plugins tracker yelp \
      openjdk-7-jre libreoffice-base gucharmap
    $ dpkg -l | grep "^rc" | awk '{print $2}' | xargs aptitude purge -y
    $ dpkg -l | grep "gir1.2\ | gimp" | awk '{print $2}'
      | xargs aptitude purge -y
    $ aptitude purge argyll argyll-ref colord colord-data
    $ dpkg -l | sed -n "/eject/d;/DVD/p;/CD/p" | awk '{print $2}' \
      | xargs aptitude purge -y
    $ deborphan --guess-all |xargs aptitude purge -y
~~~

### VM Configuration

Because each version of VirtualBox has a slightly different configuration, the
kernel modules need to be rebuilt with each upgrade/version.  I follwed the
instructions on [JiT Blog][jitblog].  In summary, this involves mounting the
Guest Image Additions and running the `VBoxLinuxAddons.run` script as root.

### Package Installtion

This section covers the list of default packages that I want installed to all me
to do my base level development.  It does not include an specific 

#### Key Packages

These packages are just to get the environment up and running, using i3.
autocutsel is used for managing the clipboard.  For further information on the
issues, please see [Subtleties of tghe X Clipboard][xclip] and [Vim, X11 and
the clipboard (Copy, paste)][vimxclip].  The Debian packages build tools are
needed to build things like the VirtualBox client packages.

_NB:_ The XDG packages may already be installed with Jessy, but I didn't note if
they were or not.

~~~ bash
    $ aptitude install i3 netselect-apt slim autocutsel
    $ aptitude install xdg-utils xdg-user-dirs
    $ aptitude install dpkg-buildpackage
    $ aptitude install dh_make git-buildpackage
    $ aptitude install rxvt-unicode-256color
    $ aptitude install dh-make git-buildpackage
    $ aptitude install dkms build-essential
~~~

The default terminal also needs to be changed to rxvt-unicode, which can be
done by:

~~~ bash
    $ sudo update-alternatives --config x-terminal-emulator
    $ sudo aptitude purge xterm
~~~

#### Other Packages

##### Atom

I occasionally need to use a GUI, non-modal, text editor (yes ther are some
times it is easier).  For this I use Atom, which can be installed by following
the instructions from the [Atom GitHub site](https://github.com/atom/atom).  I
have duplicated the instructions here for simplicity.

_NB:_ Currently only a 64-bit version is available.
 
1. Download atom-amd64.deb from the [Atom releases page](https://github.com/atom/atom/releases/latest).
1. Run `sudo dpkg --install atom-amd64.deb` on the downloaded package.
1. Launch Atom using the installed atom command.

The Linux version does not currently automatically update so you will need to

repeat these steps to upgrade to future releases.

##### RipGrep

[RipGrep][rip] is a grep replacement written in [Rust](http://www.rust-lang.org/).
It is purportedly faster than grep, but also allows for filtering by file type.o

1. Download the latest version of [RipGrep][rip-rel] for x86_64.
1. Run the installation steps below, noting that there are some bits you will need to change.

~~~bash
    $ tar zxf ripgrep-<version>-x86_64-unknown-linux-musl.tar.gz 
    $ cd ripgrep-<version>-x86_64-unknown-linux-musl/
    $ fpm -s dir -t deb -e -n ripgrep --category Utilities --license Unlicence \
      --description "ripgrep is a line oriented search tool that combines the usability of The Silver Searcher (an ack clone) with the raw speed of GNU grep. ripgrep works by recursively searching your current directory for a regex pattern. ripgrep has first class support on Windows, Mac and Linux, with binary downloads available for every release.

      ripgrep's regex engine uses finite automata and guarantees linear time searching. Because of this, features like backreferences and arbitrary lookaround are not supported." \
      --url https://github.com/BurntShshi/ripgrep --vendor BurntSushi \
      --maintainer doychi_dev@yahoo.com.au -v <version> --iteration <iteration> \
      complete/rg.bash-completion=/etc/bash_completion.d/rg.bash-completion \
      rg=/usr/local/bin/rg
    $ sudo dpkg -i ripgrep_<version>-<iteration>_amd64.deb 
~~~


<!--
##### The Platinum Searcher

[The Platinum Searcher][pt], pt for short, is a grep replacement.

1. Ensure that the Effing Package Manger is installed (see <https://github.com/jordansissel/fpm/wiki> for further details and [Digital Ocean's tutorial](https://www.digitalocean.com/community/tutorials/how-to-use-fpm-to-easily-create-packages-in-multiple-formats)).
1. Ensure that Pandoc is installed.
1. Downloading the tar file from [pt][pt-rel] site.

~~~bash
    $ mkdir -p ~/Build/tmp
    $ sudo gem install fpm
    $ cd ~/Build
    $ wget https://github.com/monochromegane/the_platinum_searcher/releases/download/<specific_release>
    $ tar zxf pt_linux_amd64.tar.gz -C tmp
    $ rm ~/Build/tmp/pt_linux_amd64/Readme.md
    $ fpm -s dir -t deb -C ~/Build/tmp/pt_linux_amd64 \
      -n "the-platinum-searcher" -v <version> --iteration <iternation> \
      --licence MIT --category extra -e 
~~~

NB: The resulting package does report an error, but works, when installed.
-->

##### fzf 

[fzf][fzf] is a command line fuzzy searcher, similar to tools like grep.  The
installation process is documented clearing for individuals on the [fzf][fzf],
but are repeated here for the completeness of this document.o

As the installation scripts for [fzf][fzf] only install [fzf][fzf] for the user
running the installation, I have not packaged the nstallation.

~~~bash
    $ git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf
    $ ~/.fzf/install
~~~

After installing [fzf][fzf], [dots][jddots] files may need to be updated (see below).

### Apply the dots Configuration

I have been using dots for awhile now and I'm glad I set it up as part of my
previous work to ensure I always have a copy of my configuration, otherwise I
would have lost all my configuration in the crash.

As I have set dots up before, and documented it, I followed the instructions in
my [Managing Debian Dotfiles][jddots]

### Clean Up the Environment

There are a few things that need to be done to clean up the environment, such
as removing the default user from the OSBoxes image and changing the hostname.
A new user also needs to be added to administer the box, so they must be added
to the `sudo` and `vboxsf` groups.

~~~ bash
    $ useradd <username> -G sudo,vboxsf
    $ sudo userdel osboxes
~~~

Log out and login as the new user.

~~~ bash
    $ sudo vim /etc/hostname
~~~

Change the name here to the new hostname.

~~~ bash
    $ sudo vim /etc/hosts
~~~

Change osboxes to the new hostname.

~~~ bash
    $ /etc/init.d/hostname.sh restart
~~~

The instructions above for changing the host name are care of [nixCraft][host]


### Clone My Repos for Development

#### doychi.github.io

1. Install GitHub Page dependencies `aptitude install ruby ruby-dev zlib1g-dev`
1. Install the ruby bundler `gem install bundler`
1. Install Jekyll `bundle exec jekyll build --save`
1. Start Jekyll, which will install all the github pages requirements `bundle exec jekyll serve`
