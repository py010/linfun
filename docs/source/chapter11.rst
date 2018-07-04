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




Chapter 11.3.d Available Monitoring Tools IV
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^



                     **Network Monitoring Utilities**



.. csv-table:: **network** 
   :header: "Utility", "Purpose", "Package"
   :widths: 30, 50, 40

   "``$ netstat``", "Detailed networking stats", "netstat"
   "``$ iptraf``", "Gather information on network interfaces", "iptraf"
   "``$ tcpdump``", "Detailed analysis of network packets and traffic", "tcpdump"
   "``$ wireshark``,"Detailed network traffic analysis", "wireshark"

