Chapter 10. APT
^^^^^^^^^^^^^^^

For use on Debian-based systems, the APT (Advanced Packaging Tool) set of programs provides a higher level of intelligent services for using the underlying dpkg program, and plays the sam role as yum on Red Hat-based systems. The main utilities are ``apt-get`` and ``apt-cache``. It can automatically resolve dependencies when installing, updating and removing packages. It accesses external software repos synchronizing with them and retrieving and installing software as needed


Chapter 10.3 What is APT?
^^^^^^^^^^^^^^^^^^^^^^^^^

APT is not a program in itself; it stands for Advanced Packaging Tool, which includes a number of utilities, such as apt-get and apt-cache. These of course, in turn, invoke the lower level dpkg program.

The APT system works with Debian packages whose file have a .deb extension. There are many distros that have descended from debianwhich have adopted the Debian packaging system with no essential mods. In fact it is not uncommon to use a repo on more than one Debian based Linux Distribution.

Chapter 10.4 apt-get
^^^^^^^^^^^^^^^^^^^^

``apt-get`` is the main APT command line tool for package management. It can be used to install, manage and upgrade individual packages or the entire system. It can even upgrade the distribution to a completely new release, which can be a difficult task.

Chapter 10.5 Queries using apt-cache
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Queries are done using the ``apt-cache`` utility:


.. csv-table:: APT-CACHE QUERIES
   :header: "Query", "desired outcome"
   :widths: 30, 50

   "``$ apt-cache search apache2``", "Search the repo for a package named apache2"
   "``$ apt-cache show apache2``", "Display basic information about the apache2 package"
   "``$ apt-cache showpkg apache2``", "Display more detailed info on the package"
   "``$ apt-cache depends apache2``", "List all dependant packages for apache2"
   "``$ apt-file search apache2.conf``", "Search the repo for a file name apache2.conf"
   "``$ apt-file list apache2``", "List all files in the apache2 package"
   
Chapter 10.6a Installing/ removing/ upgrading I
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The ``apt-get`` program is the work horse of installing, removing and upgrading packages.

.. csv-table:: apt-get 
   :header: "Query", "desired effect"
   :widths: 30, 50

   "``$ sudo apt-get update``", "Sync the package index with their repo sources"
   "``$ sudo apt-get install [package]``", "Install new packages or update and already installed package"
   "``$ sudo apt-get remove [package]``", "Remove a package without removing its config files"
   "``$ asudo apt-get --purge remove [package]``", "Remove package and its config files"
   "``$ sudo apt-get upgrade``", "Apply all available updates to a package already installed"
   

