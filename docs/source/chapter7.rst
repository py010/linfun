Chapter 7. DPKG
===============
 
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

Chapter 7.5 Source Packages I
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In the Debian packaging system, a source package consists of at least three files:

	1. An upstream tarball, ending with .tar.gz. This is the unmodified source as it comes from the package maintainers
	2. A description file, ending with .dsc, containing the package name and other metadata, such as architecture and dependencies
	3. A second tarball that contains any patches to the upstream source and additional files created for the package and ends with a name .debian.tar.gz or .diff.gz depending on the distro.

Chapter 7.5b Source Packages II
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

For example on a Ubuntu system, download a source package, then see what files are downloaded or created:

	1. ``apt-get source logrotate``
	2. ``du -shc logrotate*``

Shows all files, file sizes and total size

Chapter 7.6 DPKG Queries
^^^^^^^^^^^^^^^^^^^^^^^^


.. csv-table:: DPKG QUERIES
   :header: "cmd", "desired outcome"
   :widths: 30, 50

   "``$ dpkg -l``", "List all packages installed"
   "``$ dpkg -L wget``", "List files in the wget package"
   "``$ dpkg -s wget``", "Show info about an installed package"
   "``$ dpkg dpkg -I webfs_1.21+ds1-8_amd64.deb``", "Show info about a package file"
   "``$ dpkg -c webfs_1.21+ds1-8_amd64.deb``", "List files in a package file"
   "``$ dpkg -S /etc/init/networking.conf``", "Show what package owns /etc/init/networking.conf"
   "``$ dpkg -s wget``", "Show the status of a package"
   "``$ dpkg -V package``", "Verify the installed packages integrity"

Chapter 7.7 Installing/Upgrading/Uninstalling Packages
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The command:
	
	``$ sudo dpkg -i foobar.deb``

would be used for either installing or upgrading the foobar package.

If the package is not currently installed then it will be installed. If the package is newer than the one currently installed then it will be upgraded.

The command:

	``$ sudo dpkg -r package``

is used to remove all of an installed package except for its configuration files.

The command:

	``$ sudo dpkg -P package``

is used to remove all of an installed package including its config files (Note that -P stands for purge)



