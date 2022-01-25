## Using private patches and libs
In most cases you can use vcpkg's default version of a library right out of the box with no modifications. If you are happy with that, you can safely skip this document. But sometimes you need to make modifications, before you can include it in your project.

Perhaps you've discovered and fixed a bug in a library, but your patch has not yet been accepted. Or you need to compile a library with a specific set of compiler switches. Or you want to use vcpkg to share your own, closed-source library with your team.

In all cases you have custom "port" files and need a way to tell vcpkg to use these, rather than the build-in ones.

To do so, you have a couple of different options.

- [overlay ports](#overlay-ports), i.e. custom port files in a separate folder
- [private fork](#private-fork) of the vcpkg repository
- [registries](#registries)

Each method has its pros and cons.

### overlay ports
An _overlay port_ overrides the vcpkg build instructions with your own private instructions.

| Pros                                          | Cons                                           |
|-----------------------------------------------|------------------------------------------------|
| Easy to understand                            | Requires a commandline switch to vcpkg         |
| A single directory with a few files           | Ignores manifests (versioning)                 |
| Easily added to your projects repository      | Copy&Paste for all projects that use this port |
| self-contained, just your projects repository |                                                |

### private fork
vcpkg contains a list of all libraries known to it. This is called the "built-in registry". It is located in two directories in the vcpkg git repository:
- ./ports contains all _current_ port files. This is used in "classic" mode.
- ./versions contains all ports files of all versions up to the _current_ version. This is used in "manifest" mode.

| Pros                                          | Cons                                           |
|-----------------------------------------------|------------------------------------------------|
| No unrelated files for a specific project     | Only one central location for all private ports |
| A central location for all private ports      | Potential merge conflicts with upstream vcpkg merges |
| Supports version control and baselines        | Requires an additional repository |


### registries
With "registries" you can specify additional lists of libraries or port files, which are looked up before the "build-in registry" is queried. Like the "build-in registry", a custom package registry contains two directories:
- ./ports contains all _current_ port files for this particular registry.
- ./versions contains all port files of all versions for this particular registry.

