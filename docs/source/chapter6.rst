Chapter 6. THE RED HAT PACKAGE MANAGER RPM
==========================================

The Red Hat Package Manager (RPM) is used by a number of major distributions (and their close relatives) to control the installation, verification, upgrade, and removal of software on Linux systems. The low-level rpm program can perform all these operations, either on just one package, or on a list of packages. Operations which would cause problems (such as removing a package that another package depends on, or installing a package when the system needs other software to be installed first) are blocked from completion.

Chapter 6.3
^^^^^^^^^^^

''RPM'' (the Red Hat Package Manager) was developed (unsurprisingly) by Red Hat. All files related to a specific task are packaged into a single rpm file, which also contains information about how and where to install and uninstall the files. New versions of software lead to new rpm files which are then used for updating.

rpm files also contain dependency information. Note that unless given a specific URL to draw from, rpm in itself does not retrieve packages over the network and installs only from the local machine using absolute or relative paths.

rpm files are usually distribution-dependent; installing a package on a different distribution than it was created for can be difficult, if not impossible.

Chapter 6.4
^^^^^^^^^^^

For sys admins, RPM makes it easy to:
	1. Determine what package, if any, any file on the system is part of
	2. Determine what version is intalled
	3. Install and uninstall (erase) packages without leaving debris behind
	4. Verify that a package was installed correctly; this is useful for both troubleshooting and system auditing
	5. Distinguish doc files from the rest of the package and optionallly decide not to install them to save space.
	6. Use ftp or HTTP to install packages over the internet.

For Developers RPM offers advantages as well:
	1. Software is often made available on more than one OS. With RPM the original full and unmodified source is used as the basis, but a developer can seperate out the changes needed to build on Linux
	2. More than one architecture can be built using only one source package.


Chapter 6.5
^^^^^^^^^^^

RPM package file names are based on fields that represent specific information, as documented in the RPM standard  (http://www.rpm.org/)

The standard naming format for a binary package is:
<name>-<version>-<release>.<distro>.<architecture>.rpm
sed-4.2.1-10.el6.x86_64.rpm
The standard naming format for a source package is:
<name>-<version>-<release>.<distro>.src.rpm
sed-4.2.1-10.el6.src.rpm


Chapter 6.6
^^^^^^^^^^^

/var/lib/rpm is the default system directory which holds RPM database files in the form of  Berkeley DB hash files. The database files should not be manually modified; updates should be done only through use of the rpm program.

An alternative database directory can be specified with the --dbpath option to the rpm program. One might do this, for example, to examine an RPM database copied from another system.

You can use the --rebuilddb option to rebuild the database indices from the installed package headers; this is more of a repair, and not a rebuild from scratch.