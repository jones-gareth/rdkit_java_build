#### rdkit_java_build

A build of [RDKit](https://www.rdkit.org>) java wrappers.

Built from master branch on 9 Sep 2020 on Ubuntu 18.04.4 LTS. Statically linked to Boost 1.71.

RDKit CMake build flags:

```json
  "cmake.configureSettings": {
        "RDK_INSTALL_STATIC_LIBS": "ON",
        "RDK_BUILD_SWIG_WRAPPERS": "ON",
        "RDK_BUILD_INCHI_SUPPORT": "ON",
        "RDK_BUILD_AVALON_SUPPORT": "ON",
        "RDK_BUILD_PYTHON_WRAPPERS": "OFF",
        "RDK_BUILD_SWIG_JAVA_WRAPPER": "ON",
        "RDK_BUILD_SWIG_CSHARP_WRAPPER": "ON",
        "RDK_SWIG_STATIC": "ON",
        "BOOST_ROOT": "/home/packages/boost",
        "Boost_NO_SYSTEM_PATHS": "ON",
        "Boost_USE_STATIC_LIBS": "ON",
        "CMAKE_INCLUDE_PATH": "/home/packages/boost/include",
        "CMAKE_LIBRARY_PATH": "/home/packages/boost/lib",
        "RDK_BUILD_FREETYPE_SUPPORT": "OFF"
  }
```

Runtime dependcies of binary:

```console
$ ldd libGraphMolWrap.so
        linux-vdso.so.1 (0x00007ffe7e75a000)
        libz.so.1 => /lib/x86_64-linux-gnu/libz.so.1 (0x00007ff850d2f000)
        libpthread.so.0 => /lib/x86_64-linux-gnu/libpthread.so.0 (0x00007ff850b10000)
        libstdc++.so.6 => /usr/lib/x86_64-linux-gnu/libstdc++.so.6 (0x00007ff850787000)
        libm.so.6 => /lib/x86_64-linux-gnu/libm.so.6 (0x00007ff8503e9000)
        libgcc_s.so.1 => /lib/x86_64-linux-gnu/libgcc_s.so.1 (0x00007ff8501d1000)
        libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007ff84fde0000)
        /lib64/ld-linux-x86-64.so.2 (0x00007ff8520c9000)
```

Boost build for static linkage:

```sh
tar xzf boost_1_71_0.tar.gz
cd boost_1_71_0/
./bootstrap.sh --show-libraries
./bootstrap.sh  --with-libraries=iostreams,thread,system,serialization,regex --prefix=/home/packages/boost
./b2 cxxflags=-fPIC
./b2 cxxflags=-fPIC install
```
