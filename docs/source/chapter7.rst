Chapter 7. DPKG
^^^^^^^^^^^^^^^
 
The Debian Package Manager (DPKG) is used by all Debian-based distributions to control the installation, verification, upgrade, and removal of software on Linux systems. The low-level dpkg program can perform all these operations, either on just one package, or on a list of packages. Operations which would cause problems (such as removing a package that another package depends on, or installing a package when the system needs other software to be installed first) are blocked from completion.

Chapter 7.3 DPKG Essentials
^^^^^^^^^^^^^^^^^^^^^^^^^^^

DPKG (Debian Package) is the packaging system used to install, remove, and manage software packages under Debian Linux and other distributions derived from it. Like RPM, it is not designed to directly retrieve packages in day-to-day use, but to install and remove them locally.

Package files have a .deb suffix and the DPKG database resides in the ``/var/lib/dpkg`` directory.

Like rpm, the dpkg program has only a partial view of the universe: it knows only what is installed on the system, and whatever it is given on the command line, but knows nothing of the other available packages, whether they are in some other directory on the system, or out on the Internet. As such, it will also fail if a dependency is not met, or if one tries to remove a package other installed packages need.

Chapter 7.4 Package File Names
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Debain package file names are based on fileds that represent specific information.The standard naming format for a binary package:
	<name>_<version>-<revision_number>_<architecture>.deb

as in:

logrotate_3.8.7-1_amd64.deb

on Debian, and

logrotate_3.8.7-1ubuntu1_amd64.deb

on Ubuntu. Note that, for historical reasons, the 64-bit x86 platform is called amd64 rather than x86_64, and distributors such as Ubuntu manage to insert their name in the package name.