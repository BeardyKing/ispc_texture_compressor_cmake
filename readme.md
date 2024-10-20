# Fast ISPC Texture Compressor

#### Fork of the Intel ISPC texture compression library with added CMake support and minimal changes to the core library

### Clone

``` cmd
    git clone https://github.com/BeardyKing/ispc_texture_compressor_cmake.git
```

### CMake

``` cmake
#ISPC .exe location 
set(ISPC_COMPILER_LOCATION $ENV{ISPC_COMPILER_LOCATION})

#ISPC target
set(ISPC_COMPILER_TARGET "avx2")
#set(ISPC_COMPILER_TARGET "sse2")

add_subdirectory(ispc_texture_compressor_cmake)

target_link_libraries(target
        ispc_texture_compressor
)
```

### Library

This repository contains a texture compression library for the following
formats:

* BC6H (FP16 HDR input)
* BC7
* ASTC (LDR, block sizes up to 8x8)
* ETC1
* BC1, BC3 (aka DXT1, DXT5) and BC4, BC5 (aka ATI1N, ATI2N)

The library uses the [ISPC compiler](https://ispc.github.io/) to generate CPU
SIMD-optimized compression algorithms. For more information, see the [Fast ISPC
Texture
Compressor](https://software.intel.com/en-us/articles/fast-ispc-texture-compressor-update)
article on Intel Developer Zone.

![Sample screenshot](screenshot.png "Sample screenshot")

## License

Copyright 2017-2023 Intel Corporation

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies
of the Software, and to permit persons to whom the Software is furnished to do
so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

# DISCONTINUATION OF PROJECT #  
This project will no longer be maintained by Intel.  
Intel has ceased development and contributions including, but not limited to, maintenance, bug fixes, new releases, or updates, to this project.  
Intel no longer accepts patches to this project.  
If you have an ongoing need to use this project, are interested in independently developing it, or would like to maintain patches for the open source software community, please create your own fork of this project.  

## Contributing

Please see
[CONTRIBUTING](https://github.com/GameTechDev/ISPCTextureCompressor/blob/master/contributing.md)
for information on how to request features, report issues, or contribute code
changes.

## Build Instructions

Binaries for ISPC v1.9.2 need to be obtained separately (e.g., from [the ISPC
repo](https://ispc.github.io/downloads.html) or [the SourceForge
mirror](http://sourceforge.net/projects/ispcmirror/files/v1.9.2/)). Download
the appropriate compiler for your target, and place the binary in the following
directories:

- ISPC/linux/
- ISPC/osx/
- ISPC/win/

Source for the ISPC Texture Compressor library is under `ispc_texcomp/`.

Source for a sample that demonstrates the tradeoffs between the supported
compression variants is under `ISPC Texture Compressor/`.

#### Windows

* The build projects use Visual Studio 2017, Windows Tools 1.4.1, and the Windows 10 April 2018 Update SDK (17134)
* Use `ispc_texcomp\ispc_texcomp.vcxproj` to build the ISPC Texture Compressor library
* Use `ISPC Texture Compressor\ISPC Texture Compressor.sln` to build and run the sample

#### Mac OS X:

* The build has been tested with Xcode 7.3 with minimum OS X deployment version set to 10.9
* Use `ispc_texcomp.xcodeproj` to build the ISPC Texture Compressor library
* dylib install name is set to `@executable_path/../Frameworks/$(EXECUTABLE_PATH)`
* The sample application is not available on OS X.

#### Linux:

* Use `make -f Makefile.linux` to build the ISPC Texture Compressor library
* The sample application is not available on Linux.
