---
layout: post
title:  "S2D Cluster Updates - October 2018"
date:   2018-10-22
categories: storagespacesdirect s2d cluster hyper-converged windows-update
tags: blog
---


In my [previous blog article](https://thomassmart.github.io/storagespacesdirect/s2d/cluster/hyper-converged/windows-update/2018/10/05/s2d-cluster-updates.html), I spoke about how [recent updates](https://support.microsoft.com/en-us/help/
4103723/windows-10-update-kb4103723) had introduced some [serious bugs and reliability issues](https://support.microsoft.com/en-us/help/4462487/event-5120-with-status-io-timeout-c00000b5-after-an-s2d-node-restart-o) for S2D.


Thankfully, with the [latest October updates - KB4462928](https://support.microsoft.com/en-us/help/4462928) these have now been resolved for Windows Server 2016!
*The heavens rejoice*

If you are already running Windows Server 2019, you'll have to wait for the next round of updates, and the issues still apply to you.

## Fixes

The specific fixes are:

* Addresses an issue that occurs when using multiple Windows Server 2016 Hyper-V clusters. The following event appears in the log:

“Cluster Shared Volume 'CSVName' ('CSVName') has entered a paused state because of 'STATUS_USER_SESSION_DELETED(c0000203)'. All I/O will temporarily be queued until a path to the volume is reestablished.”

* Addresses an issue that may cause the creation of a single node cluster or the addition of more nodes to a cluster to fail intermittently.
* Addresses an issue that occurs when restarting a node after draining the node. Event ID 5120 appears in the log with a “STATUS_IO_TIMEOUT c00000b5” message. This may slow or stop input and output (I/O) to the VMs, and sometimes the nod
es may drop out of cluster membership.
* Addresses memory leak issues on svchost.exe (netsvcs and IP Helper Service).
* Addresses an issue that depletes the storage space on a cluster-shared volume (CSV) because of a Hyper-V virtual hard disk (VHDX) expansion. As a result, a Virtual Machine (VM) might continue writing data to its disk until it becomes c
orrupted or stops working. The VM might also restart and then resume writing data until a corruption occurs.

Wow! That's a lot of goodies!

## Installation

Microsoft are advocating for aggresive adoption of the October updates. Extreme caution still needs to be exercised, and a full cluster shutdown is my current advise.

I'd also suggest that you manually download the MSU and install using that.

These are my high level step suggestions

1. Download the [October MSU for Server 2016 - KB4462928 from here](http://www.catalog.update.microsoft.com/Search.aspx?q=KB4462928)

2. Copy those MSU's to each of your nodes.

3. Shutdown all VM's on the Cluster
~~~~~~~~~~~
Get-VM -ComputerName (Get-ClusterNode) | Stop-VM
~~~~~~~~~~~
4. Detach all virtual disks
~~~~~~~~~~~
Get-VirtualDisk | Disconnect-VirtualDisk
~~~~~~~~~~~
5. Shutdown the Cluster
~~~~~~~~~~~
Stop-Cluster <<CLUSTERNAME>>
~~~~~~~~~~~
6. Install all updates and reboot nodes
~~~~~~~~~~~
wusa PATH/windows10.0-kb4462928-x64_c3c3bd7c809ed0a53afab205ccbc229556f384c7.msu
~~~~~~~~~~~
*You may need to install service stack updates (SSU) before the October LCU*

7. Start the Cluster
~~~~~~~~~~~
Start-Cluster <<CLUSTERNAME>>
~~~~~~~~~~~
8. Attach all virtual disks
~~~~~~~~~~~
Get-VirtualDisk | Connect-VirtualDisk
~~~~~~~~~~~
9. Monitor storage jobs - You may also want to invoke storage jobs
~~~~~~~~~~~~~~~~~
Get-StorageJob
Get-VirtualDisk | Repair-VirtualDisk -AsJob
Get-StoragePool S2D* | Optimize-StoragePool
Get-StorageJob
~~~~~~~~~~~~~~~~~
10. Once complete power up all your VM's

Its worth noting that the update window will be considerably shorter than using SCVMM or Cluster Aware updating as there are no storage rebuilds between node reboots.
