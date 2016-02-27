---
layout: post
title:  "Debian VMs"
date:   2016-02-27 21:03
categories: debian virutal server configuration
---

Well, when I was shutting down my PC last week Windows crashed and apparently corrupted my development VM.  A very sad situation, as I didn't have backups of the virutal machine disks.  Fortunately the only thing I have really lost is the configuration, which is largely doucmented in this blog, but there are some missing bits.

This entry documents my setup for Debian this time round.  Of course I will be referencing my previous posts, where appropraite.

== References
[vbox]: https://www.virtualbox.org/ "VirtualBox"
[hv]: https://msdn.microsoft.com/en-us/virtualization/hyperv_on_windows/windows_welcome?f=255&MSPPError=-2147217396 "Hyper-V"

== Setup Overview

So at home I run Windows 10 for my desktop OS so that I can play games without any trouble.  This setup would allow me to run [Hyper-V][hv], but that would mean that the I couldn't transfer the VM to my MacBoo Pro (not that I have yet), so I have setup [VirtualBox][vbox] instead.

In rebuilding the VM this time round I decided not to install Debian from scratch.  I  hear a bunch of you asking why.  Well the answer is that I thought it would take longer.  I'm not sure whether I was right or not, but it seems to be working so far (I started writing this blog after getting most the way through the rebuild, so be warned).
