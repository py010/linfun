KNOWLEDGE CHECK Q&A
===================


CHAPTER 5 KNOWLEDGE CHECK Q&A
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Red Hat Enterprise Linux, SUSE, CentOS and Fedora use the [..........] packaging system.

	i. ``RPM``

Debian, Ubuntu and Mint use the [..........] packaging system.

	i. ``dpkg``


CHAPTER 6 KNOWLEDGE CHECK Q&A
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

``rpm -qa lists all installed packages on the system`

What rpm command would you use to verify the integrity of ``/bin/ls``?

``rpm -V coreutils``

CHAPTER 7 KNOWLEDGE CHECK Q&A
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

``dpkg -l`` lists all installed packages on the system

CHAPTER 10 KNOWLEDGE CHECK Q&A
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
``apt-get install <package>` is used to install a new package.

``apt-get update` does not accept a package as argument.

``apt-file find <file path>`` can be used to find which package provides the file specified as argument.

``apt-cache search` can be used for searching on package name and short description.

CHAPTER 11 KNOWLEDGE CHECK Q&A
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. ___________ is a debug tool that shows how a process makes requests to the operating system.
   
   a. ``strace``

2. ___________ is a tool that shows for how long the system is running.
   
   a. ``uptime``

3. ___________ is an interactive tool for monitoring process activity.

   a. ``top``

4. ___________ is a tool that displays the summary of memory usage.

   a. ``free``

5. Given a PID such as 1017, the special file __________ contains the command line used to start the process.

   a. ``/proc/[PID NUM]/cmdline``

6. What information that is not related to processes can be found at ``/proc``?
   a.
         1. The kernel commandline
         2. CPU model info
         3. Memory utilization stats
         4. Disk Partition info

   a2. Also includes more