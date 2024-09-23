# cmake-multi-pkg

## Overview

This is a dummy CMake setup to illustrate how to create multiple relocatable
packages from one top-level CMake where the reloctable packages install to a
nested hierarchy.

Two CMake relocatable libraries, foo and bar, are created and installed to a
location such as

```bash
<CMAKE_INSTALL_PREFIX>
  +--foo
  |    +--cmake
  |    +--include
  |    +--lib
  |
  +--bar
       +--cmake
       +--include
       +--lib
```

<br>

## Project Layout

```bash
<repo-root>
  +--top
  |   +--foo
  |   +--bar
  |
  +--test
```

<br>

## Overview

The _**foo**_ library creates a simple library with multiple header and source
files. It provides two functions `foo1()` and `foo2()` which print the name of
the function called.

The _**bar**_ library is the same as the _**foo**_ library but using the string
bar instead of foo.

These libraries are simple. Their purpose is to illustrate multiple files in a
relocatable CMake package.

The _**test**_ library tests the relocatable packages.


<br>

## Compilation

**Create/Compile/Install the libraries.**

The following commands will cause the test libraries to be created and
installed into a folder named `INSTALL` under the `repository-root` folder.

The following instructions assume compilation on Windows platform with Visual
Studio.

Start in the `<repository-root>` folder

```bash
cmake top -B BUILD
cmake --build BUILD
cmake --install BUILD --prefix %CD% --config debug
```

**Create/Compile the test executable.**

The test executable logic requires that the test libraries be installed to the
`INSTALL` folder in the `repository-root`.

```bash
cmake test -B BUILDTEST
cmake --build BUILDTEST
```


