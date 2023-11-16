# Build System

## Creating a project

New projects can be created using the ``new`` command. This generates a new directory that contains
the basic structure of a Banjo project:

```
banjo new name
```

## Building a project

Projects can be built using the ``build`` command. This invokes the compiler and linker to generate
the executable/library. The resulting binary can be found at ``output/<target>-<config>/<name>```:

```
banjo build
```

To run an executable immediately after building, use the ``run`` command:

```
banjo run
```

Projects can be built with the ``debug`` (default) or ``release`` config :

```
banjo build --config debug
banjo build --config release
```

## Cross-compilation

```{note}
Cross-compilation requires you to have the LLD linker installed.
```

The build system is capable of cross-compiling for targets (platforms) other than the host target:

```
banjo build --target x86_64-linux
banjo build --target aarch64-macos
```

These are the targets currently supported:  
  - ```x86_64-windows```
  - ```x86_64-linux```
  - ```x86_64-macos```
  - ```aarch64-linux```
  - ```aarch64-macos```

### Notes

Cross-compilation has some limitations depending on the target operating system.

#### Windows
Cross-compilation is currently not possible for Windows as this platform requires linking proprietary static
libraries distributed by Microsoft.

#### Linux
When cross-compiling for Linux, precompiled versions of ```glibc``` and ```libgcc``` are downloaded to
the toolchains directory. Some parts of these libraries are missing, which might cause linker errors.

#### macOS
When cross-compiling for macOS, a JSON file describing the macOS system APIs is downloaded. The build system
then generate a sysroot containing [TAPI files](https://github.com/apple-oss-distributions/tapi) from this
JSON file that the linker uses to link macOS system libraries and frameworks. The sysroot generated is
incomplete and some frameworks cannot be linked for this reason.

Toolchains
==========

The build system requires a toolchain to build projects. This includes an assembler, a linker and
system libraries.

When building for a target, the build system tries to auto-detect toolchains based
on standard paths, environment variables and the Windows registry. If a toolchain can't be found
(for example if you are cross-compiling), the build system tries to download it.
If this also fails, the toolchain has to be added manually by running the ```toolchain add``` command and specifying the config parameters:

```
banjo toolchain add x86_64-windows
banjo toolchain add aarch64-macos
```

The stored toolchains can be listed using the ``toolchain list`` command:

```
banjo toolchain list
```