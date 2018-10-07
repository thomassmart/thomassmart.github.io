---
layout: post
title:  "Hyper-V CPU Scheduler Types"
date:   2018-10-07
categories: hyper-v cpu-scheduler
tags: blog
---

# Partitions

When Hyper-V is installed in server OS' the way that Windows handles CPU operations changes significantly. Once installed, workloads a separated into 'Partitions' and the CPU operations within these partitions are sent to the hypervisor scheduler. Each virtual machine that is in operation creates a child partition and the Hyper-V machine lives within a parent partition.

This is best described in the image below

![ Child and Parent Partition Hyper-V ]({{ site.url }}/assets/img/cpuscheduler/Partitions.png)

The root partition is in fact a VM! This root partition has significantly more privileges than that of a standard VM, and also orchestrates management of VM (Through the VM worker processes and VM Management Service).

# CPU Scheduler

Up until now there has only been a single, 'fair share' scheduler. The scheduler takes the CPU operations from partitions - Virtual Processors (VP's) and distributes them to physical logical processors (LP's). The scheduler resides within the hypervisor level in the above image.

The fair share scheduler has served us well for many years, with its round robing sharing mechanism. Unfortunately it relies on assuming that isolation is adhered to at the CPU during operations.

Simultaneous multithreading (SMT), which is also known as Hyper-Threading in Intel World, allows processors to parallelize operations from multiple threads through time division, this results in a an increase in performance.
![ Hyper Threading Hyper-V ]({{ site.url }}/assets/img/cpuscheduler/hyperthreading.png)

 In recent times SMT has suffered from some serious security vulnerabilities that no longer allows us to assume that workloads are isolated once sent to the CPU.

 * [Intel L1 Terminal Fault (L1TF)](https://www.intel.com/content/www/us/en/architecture-and-technology/l1tf.html)
  * [Meltdown and Spectre - Which affects many vendors, Intel and AMD included.](https://meltdownattack.com/)

Microsoft has worked with Vendors to resolve these issues, with numerous Windows Updates, often containing CPU microcode attempting to resolve the critical vulnerabilities. Regardless of if these issues are resolved, we can no longer assume that the CPU is secure enough to handle sensitive workloads.

Microsoft has recognised this and has created new CPU schedulers, which are available within Update 2018.07 C on Server 2016 and Server 2019.

The new schedulers are:

* 'Classic'  - Traditional round robin scheduler that we all know
* 'Core'     - Offers stronger boundries through the constraining of VP's to LP's. Over subscription isn't possible
* 'Root'      - Default in Windows 10, the scheduling is handled by the root partition, rather than the hypervisor.



| CPU Scheduler Type | Performance | Security |
| ----- | ----- | ----- |
| 'Classic' | Good, allows for generous over-subscription | Low - SMT is utilised and though workloads are in separated partitions, the partition VP's can run parallelized on LP's |
| Core Scheduler - Host SMT Enabled | Reduced compared to Classic, due to VP's being bound to LPs. SMT is exposed to the VM | Stronger as child partitions VP's are isolated for all other partitions VP's and are assigned to LP's |
| Core Scheduler - Host SMT Disabled | Reduced even more compared to Classic  | Stronger again as operations within the child partition can't leak across VP's within the same partition |
| Root Scheduler | Reduced | Workloads are exposed to the root partition, however workload can be analysed by Windows Defender Application Guard, so your call on this one. |

## Performance Testings
Coming soon.
