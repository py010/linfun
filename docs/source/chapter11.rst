Chapter 11. System Monitoring
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


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
   "``$ numastat``", "Infoo about NUMA (Non-Uniform Memory Architecture", "numactl"
   "``$ strace``", "Information about all system calls a process makes", "strace"