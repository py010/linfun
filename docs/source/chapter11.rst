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
   :width: 600px
   :height: 300px
   :align: centre

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