# CarlaCppLibrary

A prebuilt Linux x86-64 build of the **CARLA 0.9.16 C++ client library**
(`libcarla_client`) together with the headers and static/shared libraries it is
built against, packaged as a ready-to-use install prefix.

CARLA doesn't distribute its C++ API in its packages unless you build from source, 
so this is meant to remove the need to compile from source.

> **This is an unofficial redistribution.** It is not affiliated with, endorsed
> by, or released by the CARLA project, the Computer Vision Center (CVC), or the
> Universitat Autònoma de Barcelona (UAB). The name "CARLA" is used only to
> identify the upstream software. For the real project, go to
> **<https://github.com/carla-simulator/carla>**.


## Contents


### Build information

| | |
|---|---|
| CARLA version | 0.9.16 |
| Platform | Linux, ELF 64-bit x86-64 |
| Compiler | GCC 9.4.0 (Ubuntu 9.4.0-1ubuntu1~20.04.2), i.e. Ubuntu 20.04 |
| Boost | 1.84.0, including the Boost.Python variant built against **Python 3.8** |
| Not included | zlib (resolved from the system), Unreal Engine headers, `carla/rss/` |

## Usage

Point your build at the prefix and link the static archives:

```cmake
set(CARLA_DIR /path/to/CarlaCppLibrary/Linux/libcarla-install)

target_include_directories(my_target PRIVATE
        ${CARLA_DIR}/include
        ${CARLA_DIR}/include/system)

target_link_directories(my_target PRIVATE ${CARLA_DIR}/lib)

target_link_libraries(my_target PRIVATE
        -Wl,-Bstatic
        carla_client rpc boost_filesystem
        -Wl,-Bdynamic
        png Recast Detour DetourCrowd
        pthread)
```

Because the libraries were built with GCC 9 and the C++11 ABI of that toolchain,
consuming code should be compiled with a compatible compiler and standard
(CARLA's client targets C++14).

## License 
This repository is an unmodified redistribution of the CARLA 0.9.16 C++ client
library (LibCarla) and the third-party dependencies it is built against. It
contains no original code: every file under Linux/ was produced by the upstream
CARLA build and is redistributed verbatim.

The MIT license above is the license of that primary work, CARLA, and applies to
the contents of Linux/libcarla-install/include/carla/ and to the compiled
library Linux/libcarla-install/lib/libcarla_client.a.

Other bundled components are licensed separately, under other permissive terms
(Boost Software License 1.0, Apache License 2.0, the zlib license, the libpng
license, and 2-clause BSD). Their full license texts are reproduced in
THIRD_PARTY_LICENSES/, and NOTICE maps each component to its license, lists the
required attributions, and records which binaries in Linux/libcarla-install/lib/
correspond to which component.

This distribution is unofficial and is not affiliated with, endorsed by, or
released by the CARLA project or by CVC/UAB. See README.md.

