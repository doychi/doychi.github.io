---
layout: post
title:  "Converting from Hyper-V to VirutalBox"
date:   2014-11-20 21:19:01
categories: virtual server
---

This article has been transfered from my other notes.

I have been using Hyper-V under Windows 8 Pro to run my virutal machines (VMs).
This is a good approach and easy to implement and ensure that the VMs are
started when the PC starts.  Unfortunately I also have a Mac that I want to be
able to share VMs with and Hyper-V won't run on a Mac (obviously).


## References

[hyperv]: http://www.hanselman.com/blog/SwitchEasilyBetweenVirtualBoxAndHyperVWithABCDEditBootEntryInWindows81.aspx "How to create a start menu which enables/disables Hyper-v" 
[vboxraw]: http://agnipulse.com/2009/07/boot-your-usb-drive-in-virtualbox/ "Create a raw device mapping for VirtualBox in Windows."
[windev]: http://ardamis.com/2012/08/21/getting-a-list-of-logical-and-physical-drives-from-the-command-line/ "List hard drive device IDs in Windows."
[service]: http://www.windows-noob.com/forums/index.php?/topic/4931-have-virtualbox-vms-start-as-a-service-on-a-windows-host/ "VmServiceControl"

1. [Enable/Disable Hyper-v] [hyperv]
1. [VirtualBox Raw Devices and Windows] [vboxraw]
1. [List hard drive device IDs in Windows] [windev]
1. [Virtual Box Servcies Management] [service]


## Tasks

1. Install VirutalBox
1. Configure the Windows boot process, as per [1].
1. Try to create the raw mappings, as per [2], you can use [3] to identify the
   device IDs.
1. Rebooting the PC released the drives.
1. VirtualBox had to be run as Administrator.

**NB:**  I after step 3 I though that Hyper-V may have been causing issues accessing the raw disks.  This wasn't the case, but to test I did uninstall Hyper-V.

### Starting VirtualBox Guests on Boot
The [VmServiceControl] [service] software doesn't seem to work very well but it
does work.  I'll have to see if I can find a wrapper for creating services that
I can place around the VirutalBox command line tools.
