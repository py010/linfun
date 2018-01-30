Chapter 5 Package Management Systems
====================================


Chapter 5.1
^^^^^^^^^^^

Chapter 5.2
^^^^^^^^^^^

Chapter 5.3 Software Packaging Concepts
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Package management systems supply the tools that allow system administrators to automate installing, upgrading, configuring and removing software packages in a known, predictable and consistent manner. 

These systems:

Gather and compress associated software files into a single package (archive), which may require one or more other packages to be installed first.​

Allow for easy software installation or removal.​

Can verify file integrity via an internal database.​

Can authenticate the origin of packages.​

Facilitate upgrades.​

Group packages by logical features.​

Manage dependencies between packages.

A given package may contain executable files, data files, documentation, installation scripts and configuration files. Also included are metadata attributes such as version numbers, checksums, vendor information, dependencies, descriptions, etc.

Upon installation, all that information is stored locally into an internal database which can be conveniently queried for version status and update information.

Chapter 5.4 Why Use Packages
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^     
Software package management systems are widely seen as one of the biggest advancements Linux brought to enterprise IT environments. 
By keeping track of files and metadata in an automated, predictable and reliable way, system administrators can use package management systems to make their installation processes scale to thousands of systems without requiring manual work on each individual system. 

Features include:

Automation:  No need for manual installs and upgrades.
Scalability:  Install packages on one system, or 10,000 systems.
Repeatability and predictability.
Security and auditing.

Chapter 5.5 Package Types
^^^^^^^^^^^^^^^^^^^^^^^^^

Packages come in several different types:

Binary packages contain files ready for deployment, including executable files and libraries. These are architecture-dependent and must be compiled for each type of machine.

Source packages are used to generate binary packages; one should always be able to rebuild a binary package (for example, by using rpmbuild --rebuild on RPM-based systems) from the source package. One source package can be used for multiple architectures.

Architecture-independent packages contain files and scripts that run under script interpreters, as well as documentation and configuration files.

Meta-packages are essentially groups of associated packages that collect everything needed to install a relatively large subsystem, such as a desktop environment, or an office suite, etc.
Binary packages are the ones that system administrators have to deal with most of the time.

On 64-bit systems that can run 32-bit programs, one may have two binary packages installed for a given program, perhaps one with x86_64 or amd64 in its name, and the other with i386 or i686 in its name.

Source packages can be helpful in keeping track of changes and source code used to come up with binary packages. They are usually not installed on a system by default, but can always be retrieved from the vendor. 


Chapter 5.6 Available Package Management Systems
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

There are two very common package management systems:

RPM (Red Hat Package Manager)
This system is used by all Red Hat-derived distributions, such as Red Hat Enterprise Linux, CentOS, Scientific Linux and CentOS, as well as by SUSE and its related community openSUSE distribution.
dpkg (Debian Package)
This system is used by all Debian-derived distributions ,including Debian, Ubuntu and Linux Mint.
There are other package management systems, such as portage/emerge used by Gentoo, pacman used by Arch, and specialized ones used by Embedded Linux systems and Android.

Another ancient system is just to supply packages as tarballs without any real management or clean removal strategies; this approach still marks Slackware, one of the oldest Linux distributions.