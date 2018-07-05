Chapter 11. SYSTEM MONITORING
=============================


Chapter 11.3 Available Monitoring Tools I
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Linux distros come with many standard performance and profiling tools already installed. Many of them are familiar from other UNIX-like operating systems, while some were developed specifically for Linux.

Most of these tools make use of mounted psuedo-filesystems, especially /proc and /sys

While there are also a number of gui monitoring tools we will  only consider the cmd line options




.. csv-table:: Available Tools 
   :header: "Utility", "Purpose", "Package"
   :widths: 30, 50, 40

   "``$ top``", "Process activity, dynamically updated", "procps"
   "``$ uptime``", "How long the system is running and the average load", "procps"
   "``$ ps``", "Detailed info about processes", "procps"
   "``$ pstree``", "A tree of processes and their connections", "procps"
   "``$ mpstat``", "Multiple processor usage", "psmisc (or pstree)"
   "``$ iostat``", "CPU utilization and I/O stats", "sysstat"
   "``$ sar``", "Display and collect info abot system activity", "psysstat"
   "``$ numastat``", "Info about NUMA (Non-Uniform Memory Architecture)", "numactl"
   "``$ strace``", "Information about all system calls a process makes", "strace"

Chapter 11.3 Available Monitoring Tools III
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Summary of the main memory and I/O monitoring utility tools:

							**Memory Monitoring Utilities**



.. csv-table:: Memory 
   :header: "Utility", "Purpose", "Package"
   :widths: 30, 50, 40

   "``$ free``", "Brief summary of memory usage", "procps"
   "``$ vmstat``", "Detailed virtual memory statistics and block I/O, dynamically updated", "procps"
   "``$ pmap``", "Process memory map", "procps"


^^^^


							**I/O Monitoring Utilities**


.. csv-table:: I/O 
   :header: "Utility", "Purpose", "Package"
   :widths: 30, 50, 40

   "``$ iostat``", "CPU utilization and I/O statistics", "sysstat"
   "``$ sar``", "Display and collect information about system activity", "systat"
   "``$ vmstat``", "Detailed virtual memory statistics and block I/O, dynamically updated", "procps"




Chapter 11.3 Available Monitoring Tools IV
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


                     **Network Monitoring Utilities**


.. csv-table:: Network 
   :header: "Utility", "Purpose", "Package"
   :widths: 30, 50, 40

   "``$ netstat``", "Detailed networking statistics", "sysstat"
   "``$ iptraf``", "Gather information on network interfaces", "iptraf"
   "``$ tcpdump``", "Detailed analysis of network packets and traffic", "tcpdump"
   "``$ wireshark``", "Detailed network traffic statistics", "wireshark"



Chapter 11.4 The /proc and /sys Psuedo-filesystems
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The /proc and /sys psuedo-filesystems contain a lot of information about the system. Furthermore, many of the entries in these directory trees are writable and can be used to change system behavior; in most cases this requires a root user.

These are psuedo-filesystems because they exist totally in memory; if you look at the disk partition when the system is not running, there will be only empty directory which is used as a mount point.
Furthermore, the information displayed is gathered only when it is looked at; there is no constant or periodic polling to update entries.



Chapter 11.5 /proc basics
^^^^^^^^^^^^^^^^^^^^^^^^^

The ``/proc`` psuedo-filesystem has a long history; it has roots in other *UNIX* operating system variants and originally was developed to display information about processes on the system, each of which has its own subdirectory in ``/proc`` with all important process characteristics available.

Over time, it grew to contain a lot of information about system properties, such as interrupts, memory, networking, etc.


Chapter 11.6 A survey of /proc I
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

What resides in the ``/proc`` psuedo-filesystem:


.. image:: https://github.com/py010/linfun/blob/master/docs/source/images/lsprocubuntu.png?raw=true
   

Chapter 11.6.b A survey of /proc II
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

First is a subdirectory for each process on the system, whether they are running, sleeping or sheduled out.

Here is the display of ``ls -F /proc/3589`` (a random process). 

   The ``-F`` option will display a '/' immediately after each pathname that is a directory, an asterisk '*' after each that is executable, an at sign '@' after each symbolic link, an equals sign '=' after each socket, a percent sign '%' after each whiteout, and a vertical bar'|' after each that is a FIFO

.. image:: https://github.com/py010/linfun/blob/master/docs/source/images/lsproc3589.png?raw=true


Chapter 11.6.c A survey of /proc III
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This directory is full of information about the status of the process and the resources it is using.

ie:

.. image:: https://github.com/py010/linfun/blob/master/docs/source/images/procstatus.png?raw=true


Chapter 11.6.d A survey of /proc IV
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Other entries give system wide info. For example, you can see the *interrupt* statistics here:


.. image:: https://github.com/py010/linfun/blob/master/docs/source/images/procinterrupts.png?raw=true

For each interrupt, we can see what the type is, how many times it has been handled on each CPU and which devices are registered to respond to it. We also get global statistics.



Chapter 11.7.a /proc/sys I
^^^^^^^^^^^^^^^^^^^^^^^^^^

Most of the tunable parameters can be found in the subdirectory tree rooted at ``/proc/sys``:


.. image:: https://github.com/py010/linfun/blob/master/docs/source/images/procsys.png?raw=true


Chapter 11.7.b /proc/sys II
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Each of these subdirectories contains information, as well as knobs that can be tuned (with care):

* ``abi/``
   Contains files with applicatin binary information; rarely used.

* ``debug/``
   Debugging parameters; for now, just some control of exception reporting.

* ``dev/``
   Device parameters, including subdirectories for **cdrom**, **scsi**, **raid**, and **parport**.

* ``fs/``
   Filesystem parameters, including quota, file handles used, and maximums, inode and directory information etc.

* ``kernel/``
   Kernel parameters. Many important entries here.

* ``net/``
   Network parameters, including subdirectories for **ipv4**, **netfilter**, etc.

* ``vm/``
   Virtual memory parameters, many important entries here.


Chapter 11.7.c /proc/sys III
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Viewing and changing the parameters can be done with simple commands, For example, the maximum number of threads allowed on the system can be seen by looking at:

``$ ls - l /proc/sys/kernel/threads-max``
``$ cat /proc/sys/kernel/threads-max``
``129498``

We can then modify and verify the change was effected:

``$ sudo bash -c 'echo 100000 > /proc/sys/kernel/threads-max'``
``$ cat /proc/sys/kernel/threads-max``
``100000``

Remeber from **sysctl** the same effect is accomplished by:

``$ sudo sysctl kernel.threads-max=100000``

Viewing the value can be done as a normal user, while changing it requires superuser privilege.


Chapter 11.8 /sys Basics
^^^^^^^^^^^^^^^^^^^^^^^^

The /sys pseudo-filesystem is an integral part of what is termed the **Unified Device Model**. Conceptually, it is based on a **device tree** and one can walk through it and see the buses, devices, etc. It also now contains information which may or may not be strictly related to devices, such as kernel modules.

It has a more tightly defined structure than does ``/proc``. Most entries contain only one line of text, although there are exceptions, unlike its antecedent, which has many multi-line entries whose exact contents have been known to change between kernel versions. Thus, the interface is hopefully more stable.

There are system properties which have display entries in both ``/proc`` and ``/sys`; for compatibility with widely used system utilities, the older forms are only gradually being whittled down.


Chapter 11.9.a A Survey of /sys I
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Support for the sysfs virtual filesystem is built into all modern kernels, and it should be mounted under /sys. However, the unified device model does not require mounting sysfs in order to function.

Let's take a look at what can be found using the 3.18 kernel; we warn you that the exact layout of this filesystem has a tendency to mutate. Doing a top level directory command yields:

``$ ls -F /sys``
``block/ bus/ class/ dev/ devices/ firmware/ fs/ kernel/ module/ power/``

which displays the basic device hierarchy. The device model sysfs implementation also includes information not strictly related to hardware.


Chapter 11.9.b A Survey of /sys II
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Network device can be examined with:


.. image:: https://github.com/py010/linfun/blob/master/docs/source/images/sysclassnet.png?raw=true


Chapter 11.9.c A Survey of /sys III
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can view the Ethernet card as shown below, the intention with sysfs is to have one text value per line, although this is not expected to be rigorously enforced.

.. image:: https://github.com/py010/linfun/blob/master/docs/source/images/sysclassnetcard.png?raw=true


Chapter 11.9.c A Survey of /sys IV
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The underlying device and driver for the first network interface can be traced through the **device** and the **driver** *symbolic links*. The screenshot here shows us what we can see when looking at the directory corresponding to the first Ethernet card.

.. image:: https://github.com/py010/linfun/blob/master/docs/source/images/sysclassnetcarddevice.png?raw=true


Chapter 11.10.a sar I
^^^^^^^^^^^^^^^^^^^^^

**sar** stands for System Activity Reporter. Its an all-purpose tool for gathering system activity and performance data and creating reports readable by humans.

On Linux systems, the backend to **sar** is **sadc** (system activity data collector), which actually accumilates the stats. Its stores info in ``/var/log/sa`` directory, with a daily frequency by default, which can be adjusted. Data collection can be started from the command line, and regular periodic collection is usually started as a cron jon stored in ``/etc/cron.d/sysstat``

**sar** then reads in this data and then produces a report.

**sar** is invoked via:

``$ sar [ options ] [ interval ] [ count ]``

With no options given a report on CPU usage will be given.

.. image:: https://github.com/py010/linfun/blob/master/docs/source/images/sar.png?raw=true


Chapter 11.10.b sar II
^^^^^^^^^^^^^^^^^^^^^^
List of the major **sar** options, each one has its own sub-options:

.. csv-table:: sar options 
   :header: "option", "meaning"
   :widths: 30, 60

   "``$ -A``", "Almost all information"
   "``$ -b``", "I/O and transfer rate stats (similar to ``iostat``)"
   "``$ -B``", "Paging statistics including page faults"
   "``$ -x``", "Block device activity (similar to ``iostat -x``"
   "``$ -n``", "Network statistics"
   "``$ -P``", "Per CPU statistics (as in ``sar -P ALL 3``)
   "``$ -q``", "Queue lengths"
   "``$ -r``", "Swap and memory utilization stats"
   "``$ -R``", "Memory statistics"
   "``$ -u``", "CPU utilization"
   "``$ -v``", "Statistics about inodes and files and file handles"
   "``$ -w``", "Context switching statistics"
   "``$ -W``", "Swapping statistics, pages in and out per second"

Chapter 11.10.c sar III
^^^^^^^^^^^^^^^^^^^^^^^

This screenshot demonstrates how to get paging statistics and the I/O transfer rate stats.

.. image:: https://github.com/py010/linfun/blob/master/docs/source/images/sario.png?raw=true

The **ksar** program is a java-based utility for generating nice graphs of **sar** data. It can be downloaded from  http://sourceforge.net/projects/ksar.
