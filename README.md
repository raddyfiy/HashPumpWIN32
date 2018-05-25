# HashPump (WIN32)

A tool to exploit the hash length extension attack in various hashing algorithms.

Currently supported algorithms: MD5, SHA1, SHA256, SHA512.

Slightly modified to compile on WIN32 using CMake as build system. Current CMakeLists.txt will work only on Windows. Be bad, enjoy.

Forked from https://github.com/bwall/HashPump

Used code from:
* https://www.codeproject.com/Articles/157001/Full-getopt-Port-for-Unicode-and-Multibyte-Microso
* https://stackoverflow.com/questions/341817/is-there-a-replacement-for-unistd-h-for-windows-visual-c/826027#826027


## Building HashPump on Windows

Get the dependencies you will need:

* Compiled libraries OpenSSL for WIN32: https://github.com/openssl
* Python 3.6: https://www.python.org/downloads


### Building OpenSSL (WIN32)

Clone it. To compile it you've to install:

* ActivePerl (I used v5.24.3): https://www.activestate.com/activeperl
* NASM (I used 2.13.03): https://www.nasm.us
* nmake (I used 14.11.25548.2)

**Be sure to have the above tools at your PATH**

Execute *Developer Command Prompt* (in my case for VS 2017) and do the following:

```powershell
cd path/to/openssl_code
perl Configure VC-WIN32 --prefix=C:/user/dev/openssl --openssldir=C:/user/dev/ssl
nmake
nmake test
nmake install
```

It is recommended to set the *prefix* and *openssldir* to user's directory. If not, be sure you've access to the default paths; in my experience the most OpenSSL compiling problems on Windows are regarding paths and permissions.

For more info about OpenSSL building on Windows, check:
* https://github.com/openssl/openssl/blob/OpenSSL_1_1_0-stable/INSTALL 
* https://github.com/openssl/openssl/blob/OpenSSL_1_1_0-stable/NOTES.WIN


## Compile HashPump on Windows

The easiest way is to set up the following environmet variables, the CMake script will use it to set up the linker.

* OPENSSL_ROOT_DIR -> Path to compiled OpenSSL library (e.g. C:/user/dev/openssl)
* PYTHON36_ROOT_DIR -> Path to your Python 3.6 installatin (e.g. C:/Python36-32)

Just set the source code path of HashPumpWIN32 and it's output path, configure and generate the project. I compiled it using Visual Studio 2017 Community Edition. On Linux *make* should work too without changes.
