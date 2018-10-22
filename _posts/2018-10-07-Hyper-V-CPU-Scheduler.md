---
layout: post
title:  "Hyper-V CPU Scheduler Types"
date:   2018-10-07
tags: hyper-v cpu-scheduler server-2016 server-2019
published: false
---

Recent security vulnerabilities within CPU's have resulted in a need to change some fundamental CPU scheduling within Hyper-V so to keep VM's secure. [Microsoft has an article outlining the different schedulers now available](https://docs.microsoft.com/en-us/windows-server/virtualization/hyper-v/manage/manage-hyper-v-scheduler-types). This blog article is to help with understanding the schedulers, how they work and perform, as well a briefly explaining how Hyper-V virtualises CPU resources.

# Partitions

When Hyper-V is installed in server OS, the way that Windows handles CPU operations changes significantly. Once the role is installed, workloads a separated into 'Partitions' and the CPU operations within these partitions are sent to the hypervisor scheduler. Partitioning allows to keep each VM within their own container, excluding them from being aware of each other. When a VM is powered on, the hypervisor creates a child partition, for that VM. The Hyper-V host is created a root partition by the hypervisor at OS boot.

This is best described in the image below

![ Child and Parent Partition Hyper-V ]({{ site.url }}/assets/img/cpuscheduler/Partitions.png)

The Hyper-V Host root partition is in fact a VM! It is worth mentioning, that this root partition has significantly more privileges than that of a standard VM. The root partition  also orchestrates management of VM (Through the VM worker processes and VM Management Service). Partitions are managed by the hypervisor.

# CPU Scheduler

Up until now there has only been a single, 'fair share' scheduler. The scheduler takes the CPU operations from the partition's CPU Virtual Processors (VP's) and distributes them to the host's physical logical processors (LP's). The scheduler resides within the hypervisor level in the above image.

The fair share scheduler has served us well for many years, with its round robing sharing mechanism. Unfortunately the scheduler relies on assuming that each LP is completely isolated from each other LP.

Simultaneous multithreading (SMT), which is also known as Hyper-Threading in Intel World, allows processors to parallelise operations from multiple threads, this results in a an increase in modest performance.

![Simultaneous multithreading SMT Hyper Threading Hyper-V ]({{ site.url }}/assets/img/cpuscheduler/hyperthreading.png)

 In recent times SMT has suffered from some serious security vulnerabilities that no longer allows us to assume that VM's VP's are isolated once sent to the Host's LP's. Some of the most notable recent vulnerabilities are:

 * [Intel L1 Terminal Fault (L1TF)](https://www.intel.com/content/www/us/en/architecture-and-technology/l1tf.html)
 * [Meltdown and Spectre](https://meltdownattack.com/) - Which affects many vendors, Intel and AMD included.

Microsoft has worked with vendors to resolve these issues. Numerous Windows Updates, often containing CPU microcode ,attempting to resolve the critical vulnerabilities have been released. Regardless of if these issues are 100% resolved, we can no longer assume that the CPU is secure enough to handle sensitive workloads when virtualising.

Microsoft has recognised this, and has created new CPU schedulers. These new CPU hypervisor schedulers are available within Update 2018.07 C on Server 2016, Server 2019 and Windows 10..

The new schedulers are:

* 'Classic'  - Traditional round robin scheduler that we all know
* 'Core'     - Offers stronger boundries through the constraining of VP's to LP's.
* 'Root'      - Default in, and only recommended for, Windows 10. The scheduling is handled by the root partition, rather than the hypervisor. This allows for windows

| CPU Scheduler Type | Performance | Security |
| ----- | ----- | ----- |
| 'Classic' | Good, allows for generous over-subscription and performance  | Low - SMT is utilised and though workloads are in separated partitions, the partition VP's can run parallelized on LP's. This could result in one partition being privvy to the operations of a different partition |
| Core Scheduler - Host SMT Enabled | Reduced compared to Classic, due to VP's being bound to LPs. SMT is exposed to the VM | Stronger as child partitions VP's are isolated for all other partitions VP's and are assigned to LP's for operations |
| Core Scheduler - Host SMT Disabled | Roughly 1/2 compared to that of the classic scheduler.  | Stronger again as operations within the child partition can't leak across VP's within the same partition |
| Root Scheduler | I didn't benchmark this, however my understanding is that it would be lower than that of either core or classic. | Child partitions are exposed to the root partition,  workload can be analysed by Windows Defender Application Guard, so your call on this one. |


## Performance Testings
Test bench - HPE DL380 G7 (Old, but available)
* 2 x Intel Xeon E5630 - 2.53 Ghz.
  * Quad core
  * Hyperthreading capable
  * Total of 16 Logical Processors (LP's) when SMT Enabled.
  * Total of 8 Logical Processors (LP's) when SMT Disabled.
* 112 GB RAM
* 4 x 10k 120GB HDD's in RAID 1+0
* Windows Server 2016 - 1607
* 16 Virtual Machines
  * 4 VP's when host SMT is enabled.
  * 2 VP's when host SMT is disabled.
  * 4GB RAM
  * Windows Server 2016 - 1607

All test performed by using [Matrox Cinebench R17](https://www.maxon.net/en/products/cinebench/) for its simple usage, and single value scoring.

Testing is based on VP:LP ratio. This meant that when SMT was disabled, the VP's presented through to VM's were halved.

The OS' base Cinebench score is *764*

![ Cinebench SMT Hyper-V ]({{ site.url }}/assets/img/cpuscheduler/host-score.png)

The steps in each run process was to:
1. Start the required number of VM's
2. Login to every console and open Cinebench
3. Click the start on Cinebench in each VM as close as possible.
![ Hyper-V Starting Cinebench ]({{ site.url }}/assets/img/cpuscheduler/run-shot.png)
4. Wait and record results for each pass

### Classic scheduler
The classic scheduler has been the default CPU scheduler since the Hyper-V inception up until Server 2019. The classic scheduler offers the highest performance variability. VP's can be assigned to any LP's. This results in a higher availability for VP's to execute operations when LP's are available.

#### Results


### Core Scheduler - SMT Enabled

### Core Scheduler - SMT Disabled

### Comparison

## What am I running?

## How do I change scheduler?
