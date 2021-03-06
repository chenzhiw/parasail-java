# parasail-java: Java JNI Interface for the Parasail C Library

Author: Jeff Daily (jeff.daily@pnnl.gov)

## Table of Contents

  * [Installation](#installation)
  * [Code Example](#code-example)
  * [Citing parasail](#citing-parasail)
  * [License: Battelle BSD\-style](#license-battelle-bsd-style)

This package contains Java JNI bindings for [parasail](https://github.com/jeffdaily/parasail). Parasail is a SIMD C (C99) library containing implementations of the Smith-Waterman (local), Needleman-Wunsch (global), and semi-global pairwise sequence alignment algorithms.  

## Installation

[back to top]

Once you have installed [parasail](https://github.com/jeffdaily/parasail), you can then compile the Java JNI bindings.  The build uses cmake.  The easiest way for cmake to locate the parasail installation is to use the CMAKE_PREFIX_PATH variable.  See the following example for details.

```bash
cd parasail-java
mkdir build
cd build
cmake .. -DCMAKE_PREFIX_PATH=/your/path/to/parasail/install/prefix
make
```
### for MinGW
```bash
cd parasail-java
mkdir build
cd build
cmake .. -DCMAKE_LIBRARY_PATH="/path/to/parasail/build" -DCMAKE_INCLUDE_PATH="/path/to/parasail" -G "MinGW Makefiles"
gcc -shared -DMS_WIN64 -DBUILD_DLL -o JNIparasail.dll -I"%JAVA_HOME%/include" -I"%JAVA_HOME%/include/win32" -I/path/to/parasail/include JNIparasail.c /path/to/parasail/library/libparasail_static.a
```

That should produce the parasail.jar as well as the JNIparasail library, named according to your platform.  For example, libJNIparasail.jnilib on OSX, JNIparasail.dll on Windows, and libJNIparasail.so on Linux.

## Code Example

[back to top]

```java
import parasail.Aligner;
import parasail.Matrix;
import parasail.Result;

Result result = Aligner.sw_scan_16("asdf", "asdf", 11, 1, Matrix.blosum62);
System.out.println("score = " + result.getScore());
result.delete();
```

Please refer to the [parasail C library README.md](https://github.com/jeffdaily/parasail/blob/master/README.md#standard-function-naming-convention) for the naming conventions of the various functions provided.  These Java bindings drop the "parasail_" prefix since the functions are naturally namespaced within the parasail.Aligner class.

Result objects should be manually deleted when no longer used in order to free allocated memory by the parasail C library.  As with the parasail C library, gap open and gap extension penalties are specified as positive numbers.

There is a slightly more complicated code example that is compiled as part of the parasail.jar.  See [Example.java](src/parasail/Example.java).  You can run the compiled example from within the build directory by running `java -cp ./parasail.jar parasail.Example <filename.fasta>`.

## Citing parasail

[back to top]

If needed, please cite the following paper.

Daily, Jeff. (2016). Parasail: SIMD C library for global, semi-global,
and local pairwise sequence alignments. *BMC Bioinformatics*, 17(1), 1-11.
doi:10.1186/s12859-016-0930-z

http://dx.doi.org/10.1186/s12859-016-0930-z

## License: Battelle BSD-style

[back to top]

Copyright (c) 2015, Battelle Memorial Institute

1.  Battelle Memorial Institute (hereinafter Battelle) hereby grants
    permission to any person or entity lawfully obtaining a copy of this
    software and associated documentation files (hereinafter “the
    Software”) to redistribute and use the Software in source and binary
    forms, with or without modification.  Such person or entity may use,
    copy, modify, merge, publish, distribute, sublicense, and/or sell
    copies of the Software, and may permit others to do so, subject to
    the following conditions:

    - Redistributions of source code must retain the above copyright
      notice, this list of conditions and the following disclaimers.

    - Redistributions in binary form must reproduce the above copyright
      notice, this list of conditions and the following disclaimer in
      the documentation and/or other materials provided with the
      distribution.

    - Other than as used herein, neither the name Battelle Memorial
      Institute or Battelle may be used in any form whatsoever without
      the express written consent of Battelle.

    - Redistributions of the software in any form, and publications
      based on work performed using the software should include the
      following citation as a reference:

    Daily, Jeff. (2016). Parasail: SIMD C library for global,
    semi-global, and local pairwise sequence alignments. *BMC
    Bioinformatics*, 17(1), 1-11.  doi:10.1186/s12859-016-0930-z

2.  THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
    "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
    LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS
    FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL BATTELLE
    OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
    SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
    LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF
    USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND
    ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
    OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT
    OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF
    SUCH DAMAGE.

[back to top]: #parasail-java-java-jni-interface-for-the-parasail-c-library
