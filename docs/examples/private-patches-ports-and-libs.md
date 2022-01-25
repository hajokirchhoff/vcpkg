## Using private patches and libs
vcpkg comes with more than 1000 different libraries. In most cases you can use them right out of the box with no modifications. If you are happy with that, you can safely skip this document. But sometimes this default version of a library does not fit your scenario and you need to make modifications, before you can use the library in your project.

To do so, you have a couple of different options.
- overlay ports
- use a private fork of the vcpkg repository
- use registries
Each method has its pros and cons.

### overlay ports
An _overlay port_ overrides the vcpkg build instructions for this library with your own private instructions. It is basically just a directory with a couple of files in it.

### private fork of the vcpkg repository
The vcpkg git repository contains a list of all libraries known to it. This list is located in two places:
- ./ports contains all _current_ port files. This is used in "classic" mode.
- ./versions contains all ports files of all versions up to the _current_ version. This is used in "manifest" mode.



|method|pros|cons|
|-------------------------|-------------------|---------------------------------|
| overlay ports | private patch or lib per project | manual configuration per project required --overlay-port parameter |
| private fork | private patch per user or team | additional git repository for private fork required |
| registries | private patch per user, per project, per team | additional git repositories per registry required |
