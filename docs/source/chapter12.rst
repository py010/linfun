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