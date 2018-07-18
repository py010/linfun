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

Chapter 13.5.b ``/proc/sys/vm`` II (ENTRIES)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. csv-table:: Entries 
   :header: "Entry", "Purpose"
   :widths: 50, 50

   	"admin_reserve_kbytes",	"Amount of free memory reserved for privileged users"
   	"block_dump", "Enables block I/O debugging"
	"compact_memory", "Turns on or off memory compaction (essentially defragmentation) when configured into the kernel"
	"dirty_background_bytes", "Dirty memory threshold that triggers writing uncommitted pages to disk"
	"dirty_background_ratio", "Percentage of total pages at which kernel will start writing dirty data out to disk"
	"dirty_bytes", "The amount of dirty memory a process needs to initiate writing on its own"
	"dirty_expire_centisecs", "When dirty data is old enough to be written out in hundredths of a second)"
	"dirty_ratio", "Percentage of pages at which a process writing will start writing out dirty data on its own"
	"dirty_writeback_centisecs", "Interval in which periodic writeback daemons wake up to flush. If set to zero, there is no automatic periodic writeback"
	"drop_caches", "Echo 1 to free page cache, 2 to free dentry and inode caches, 3 to free all. Note only clean cached pages are dropped; do sync first to flush dirty pages"
	"extfrag_threshold", "Controls when the kernel should compact memory"
	"hugepages_treat_as_movable", "Used to toggle how huge pages are treated"
	"hugetlb_shm_group", "Sets a group ID that can be used for System V huge pages"
	"laptop_mode", "Can control a number of features to save power on laptops"
	"legacy_va_layout", "Use old layout (2.4 kernel) for how memory mappings are displayed"
	"lowmen_reserve_ratio", "Controls how much low memory is reserved for pages that can only be there; i.e., pages which can go in high memory instead will do so. Only important on 32-bit systems with high memory"
	"max_map_count", "Maximum number of memory mapped areas a process may have. The default is 64 K"
	"min_free_kbytes", 	"Minimum free memory that must be reserved in each zone"
	"mmap_min_addr", 	"How much address space a user process cannot memory map. Used for security purposes, to avoid bugs where accidental kernel null dereferences can overwrite the first pages used in an application"
	"nr_hugepages",	"Minimum size of hugepage pool"
	"nr_pdflush_hugepages", "Maximum size of the hugepage pool = nr_hugepages *nr_overcommit_hugepages" 
	"nr_pdflush_threads", "Current number of pdflush threads; not writeable"
	"oom_dump_tasks", "If enabled, dump information produced when oom-killer cuts in"
	"oom_kill_allocating_task",	"If set, the oom-killer kills the task that triggered the out of memory situation, rather than trying to select the best one"
	"overcommit_kbytes", "One can set either overcommit_ratio or this entry, but not both"
	"overcommit_memory", "If 0, kernel estimates how much free memory is left when allocations are made. If 1, permits all allocations until memory actually does run out. If 2, prevents any overcommission"
	"overcommit_ratio", "If overcommit_memory = 2 memory commission can reach swap plus this percentage of RAM"
	"page-cluster", "Number of pages that can be written to swap at once, as a power of two. Default is 3 (which means 8 pages)"
	"panic_on_oom", "Enable system to crash on an out of memory situation"
	"percpu_pagelist_fraction",	"Fraction of pages allocated for each cpu in each zone for hot-pluggable CPU machines"
	"scan_unevictable_pages", "If written to, system will scan and try to move pages to try and make them reclaimable"
	"stat_interval", "How often vm statistics are updated (default 1 second) by vmstat swappiness, How aggressively should the kernel swap"
	"user_reserve_kbytes", "If overcommit_memory is set to 2 this sets how low the user can draw memory resources"
	"vfs_cache_pressure", "How aggressively the kernel should reclaim memory used for inode and dentry cache. Default is 100; if 0 this memory is never reclaimed due to memory pressure"


Chapter 13.6.a vmstat I
^^^^^^^^^^^^^^^^^^^^^^^

```vmstat`` is a multi-purpose tool that displays information about memory, paging, I/O, processor activity and processes. It has many options. The general form of the command is:

```$ vmstat [options] [delay] [count]```

If **delay** is given in seconds, the report is repeated at that interval count times; if **count** is not given **vmstat** will keep reporting statistics forever until it is killed such as Ctl-C.

```vmstat 2 4```

.. image:: https://github.com/py010/linfun/blob/master/docs/source/images/vmstat.png?raw=true


Chapter 13.6.b vmstat II
^^^^^^^^^^^^^^^^^^^^^^^^

.. csv-table:: Available Tools 
   :header: "Field", "Subfield", "Meaning"
   :widths: 30, 50, 40

   "Processes", "r", "Number of processes waiting to be scheduled in"
   "Processes", "b", "Number of processess in uninterruptible sleep"
   "memory", "swpd", "Virtual memory used (KB)"
   "memory", "free", "Free, idle memory"
   "memory", "buff", "Buffer memory"
   "swap", "si", "Memory swapped in"
   "swap", "so", "Memory swapped out"
   "I/O", "Display and collect info about system activity", "psysstat"
   "I/O", "Info about NUMA (Non-Uniform Memory Architecture)", "numactl"
   "system", "in", "interupts/second"
   "system", "cs", "Context switches/second"
   "CPU", "st", "Time stolen from vm %"
   "CPU", "us", "CPU time running user code %"
   "CPU", "sy", "CPU time running kernel code"
   "CPU", "id", "CPU time idle"
   "CPU", "wa", "Time waiting for I/O"

Chapter 13.6.c vmstat III
^^^^^^^^^^^^^^^^^^^^^^^^^

If the option ```-S m``` is given, memory stats will be given in MB instead of KB.

With the option ```-a``, ***vmstat*** displays information about active and inactive memory, where active memory pages are thos which have been recently used; they may be **clean** (disk contents are up to date) or **dirty** (need to be flushed to disk eventually). By contrast, inactive memory pages have not been recently used and are more likely to be cleanand releasr sooner under memory pressure:

```$ vmstat -a 2 4```

.. image:: https://github.com/py010/linfun/blob/master/docs/source/images/vmstata.png?raw=true

Chapter 13.6.d vmstat IV
^^^^^^^^^^^^^^^^^^^^^^^^

To get a table of memory statistics and certain event counters use the -s option:

.. image:: https://github.com/py010/linfun/blob/master/docs/source/images/vmstats.png?raw=true

Chapter 13.6.e vmstat V
^^^^^^^^^^^^^^^^^^^^^^^^

To get a table of disk statistics use the -d option:

.. image:: https://github.com/py010/linfun/blob/master/docs/source/images/vmstatd.png?raw=true


Chapter 13.6.f vmstat VI
^^^^^^^^^^^^^^^^^^^^^^^^

.. csv-table:: vmstat Disk Fields 
   :header: "Field", "Subfield", "Meaning"
   :widths: 30, 50, 40

   "reads", "total", "Total reads completed successfully"
   "reads", "merged", "Grouped reads - resulting in one I/O"
   "reads", "ms", "Milliseconds spent reading"
   "writes", "total", "Total writes completed successfully"
   "writes", "merged", "Grouped writes"
   "writes", "ms", "Ms spent writing"
   "I/O", "cur", "I/O in progress"
   "I/O", "sec", "seconds spent for I/O"
 

Chapter 13.6.g vmstat VII
^^^^^^^^^^^^^^^^^^^^^^^^^

If you just want to get some quick statistics on only one partition, use the -p option:

.. image:: https://github.com/py010/linfun/blob/master/docs/source/images/vmstatp.png?raw=true


Chapter 13.7.a /proc/meminfo I
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
As noted earlier, a relatively lengthy summary of memory statistics resides in /proc/meminfo:

.. image:: https://github.com/py010/linfun/blob/master/docs/source/images/procmeminfo.png?raw=true


Chapter 13.7.b /proc/meminfo II
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

