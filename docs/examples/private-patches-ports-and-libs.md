## Using private patches and libs
If you are happy with vcpkg's default version of a library, you can safely skip this document.

But if you
- have a patch for a library, which is not yet contained in the official release or
- need a specific set of compiler switches with your build or
- want to share your private, closed-source library with others via the vcpkg mechanism

then you can use any of the following mechanism to tell vcpkg to use your own "port files" instead of the official ones.

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

