Chapter 13. Memory: Monitoring Usage and Tuning
===============================================

Chapter 13.3 Memory Tuning Considerations:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Tuning the memory sub-system can be a complex process. First of all, one has to take note that memory usage and I/O throughput are intrinsically related, as, in most cases, most memory is being used to cache contents of files on disk.

Thus, changing memory parameters can have a large effect on I/O performance, and changing I/O parameters can have an equally large converse effect on the virtual memory sub-system.

When tweaking parameters in ``/proc/sys/vm``, the usual best practice is to adjust one thing at a time and look for effects. The primary (inter-related) tasks are:

	1. **Controlling flushing parameters**; ie., how many pages are allowed to be dirty and how often they are flushed out to disk

	2. **Controlling *swap* behaviour**; ie., how much pages that reflect file contents are allowed to remian in memory, as opposed to those that need to be swapped out as they have no other backing store.

	3. **Controlling how much memory *overcommission* is allowed**, since many programs never need the full amount of memory they request, particularly because of copy on write (**COW**) techniques.

Memory tuning can often be subtle and what works in one system situation or load may be far from optimal in other circumstances.

Chapter 13.4 Memory Monitoring Tools:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. csv-table:: Memory Monitoring 
   :header: "Utility", "Purpose", "Package"
   :widths: 30, 50, 40

   "``$ free``", "Brief summary of memory usage", "procps"
   "``$ vmstat``", "Detailed virtual memory statistics and block I/O, dynamically updated", "procps"
   "``$ pmap``", "Process memory map", "procps"


Chapter 13.5.a ``/proc/sys/vm`` I
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The ``/proc/sys/vm`` directory contains many tunable knobs to control the **Virtual Memory** system. Exactly what appears in this directory will depend somewhat on the kernel version. Almost all of the entries are writable (by **root**).

These values can be changed either by directly writing to the entry, or using the **sysctl** utility. Furthermore, by modifying the ``/etc/sysctl.conf``, values can be set at boot time.

You can find full documentation for the ``/proc/sys/vm`` directory in the kernel source (or kernel documentation package on your distribution), usually under ``Documentation/sysctl/vm.txt``.

