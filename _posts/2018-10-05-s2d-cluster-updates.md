---
layout: post
title:  "S2D Cluster Updates - May 2018"
date:   2018-10-05
categories: storagespacesdirect s2d cluster hyper-converged windows-update
tags: blog
---

There is nothing more frustrating that doing all possible due diligence, raising the relevant Change Requests, completing testing, just to have a routine Windows Update fail. Sorry, scratch that, not fail. MONUMENTLY FAIL.

Unfortunately, within increasing demand on software through mechanisms such as SDN (Software Defined Networks), SDS (Software Defined Storage) and HCI (Hyper-converged Infrastructure) a failure can have an exponential impact on workloads.

[Introducing the Cumulative Update May 9th 2018 update](https://support.microsoft.com/en-us/help/4103723/windows-10-update-kb4103723)

If you have this update installed, and are running Storage Spaces Direct.
*EXCERCISE EXTREME CAUTION WHEN COMPLETING MAINTENANCE*

[Microsoft have an article on how you can perform update more safely](https://support.microsoft.com/en-us/help/4462487/event-5120-with-status-io-timeout-c00000b5-after-an-s2d-node-restart-o). In my experience this improved resiliency, but didn't resolve (We only had 1 node failure instead of 4, so Yay, I guess?)

This is still unresolved (As of Oct 5th), and my Microsoft Partner case is making very little progress. I'd suggest that you organise complete cluster outages to install updates.

These high level steps may help you:

1. Shutdown all VM's on the Cluster
~~~~~~~~~~~
Get-VM -ComputerName (Get-ClusterNode) | Stop-VM
~~~~~~~~~~~
2. Detach all virtual disks
~~~~~~~~~~~
Get-VirtualDisk | Disconnect-VirtualDisk
~~~~~~~~~~~
3. Shutdown the Cluster
~~~~~~~~~~~
Stop-Cluster <<CLUSTERNAME>>
~~~~~~~~~~~
4. Install all updates and reboot nodes
5. Start the Cluster
~~~~~~~~~~~
Start-Cluster <<CLUSTERNAME>>
~~~~~~~~~~~
6. Attach all virtual disks
~~~~~~~~~~~
Get-VirtualDisk | Connect-VirtualDisk
~~~~~~~~~~~
7. Monitor storage jobs - You may also want to invoke storage jobs
~~~~~~~~~~~~~~~~~
Get-VirtualDisk | Repair-VirtualDisk -AsJob
Get-StoragePool S2D* | Optimize-StoragePool
~~~~~~~~~~~~~~~~~
8. Once complete power up all your VM's

Its worth noting that the update window will be considerably shorter than using SCVMM or Cluster Aware updating as there are no storage rebuilds between node reboots.
