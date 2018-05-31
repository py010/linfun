Chapter 6 THE RED HAT PACKAGE MANAGER RPM
=========================================

The Red Hat Package Manager (RPM) is used by a number of major distributions (and their close relatives) to control the installation, verification, upgrade, and removal of software on Linux systems. The low-level rpm program can perform all these operations, either on just one package, or on a list of packages. Operations which would cause problems (such as removing a package that another package depends on, or installing a package when the system needs other software to be installed first) are blocked from completion.

Chapter 6.3
^^^^^^^^^^^

RPM (the Red Hat Package Manager) was developed (unsurprisingly) by Red Hat. All files related to a specific task are packaged into a single rpm file, which also contains information about how and where to install and uninstall the files. New versions of software lead to new rpm files which are then used for updating.

rpm files also contain dependency information. Note that unless given a specific URL to draw from, rpm in itself does not retrieve packages over the network and installs only from the local machine using absolute or relative paths.

rpm files are usually distribution-dependent; installing a package on a different distribution than it was created for can be difficult, if not impossible.