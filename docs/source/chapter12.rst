Chapter 12 Monitoring Tools (processes)
=======================================

Linux administrators make use of many utilities, such as **ps**, **pstree** and **top**, all of which have long histories in UNIX-like operating systems.


Chapter 12.4 Viewing process states with ps
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**ps** is a workhorse for displaying characteristics and statistics associated with processes, all of which are garnered from the ``/proc`` directory associated with the process.

This command utility has existed in all UNIX like operating system variants, and that diversity is relected in the complicated potpourri of options that the **linux** version of **ps** accepts, which fall into 3 categories:

	1. **UNIX** options, which must be preceded by -, and which may be grouped.
	2. **BSD** options, which must not be preceded by -, and which may be grouped.
	3. **GNU** long options, each of which must be preceded by --,

Having all these possible options can be confusing, most sys admins tend to use one or two standard combinations for their daily use.

Chapter 12.5 BSD option format for **ps**
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can see a typical usage with the BSD option format in the screenshot provided, where the aux option shows all processes. Commands which are surrounded by square brackets (as in [ksoftirqd/0]) are threads that exist totally within the kernel; if there is one for each CPU, the command is followed by the integer specifying the CPU it is running on.

.. image:: https://github.com/py010/linfun/blob/master/docs/source/images/psaux.png?raw=true

Chapter 12.6 ps Output fields I
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Most of the fields in the preceding example are self-explanatory. Of the others:

VSZ is the process' virtual memory size in KB.
RSS is the resident set size; the non-swapped physical memory a task is using in KB.
STAT describes the state of the process; in our example we see only S for sleeping, or R for running. The additional character in the state (where it exists) can be:
- < for high priority (not nice)
- N for low priority (nice)
- L for having pages locked in memory
- s for session leader
- l for multi-threaded
- + for being in the foreground process group.


Chapter 12.6.b ps Output fields II
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Adding the f option will show how processes connect by ancestry, as in:

.. image:: https://github.com/py010/linfun/blob/master/docs/source/images/psaux.png?raw=true


Chapter 12.7.a UNIX Output fields for ps I
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can see a typical usage with the UNIX option format in the screenshot provided. Note that it is now showing the Parent Process ID (PPID) and the niceness (NI). You may observe that many processes show PPID=2 in this example (taken from RHEL 7 and using systemd) an internal kernel process, kthreadd, which is designed to adopt children when the parent process dies. In older kernels and systems, you would see PPID=1 for sbin/init, but it is really the same thing going on.


.. image:: https://github.com/py010/linfun/blob/master/docs/source/images/pself.png?raw=true


Chapter 12.7.b UNIX Option format for ps II
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


Some common selection options in the UNIX format are:

	``-A or -e``
		Select all processes
	``-N``
		Negate selection (means do the opposite)
	``-C``
		Select by command name
	``-G``
		Select by real group ID (also supports names)
	``-U`` 
		Select by real user ID (also supports names).


