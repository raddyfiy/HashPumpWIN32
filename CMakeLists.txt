# HashPumpWIN32 build script (25/05/2018)
# @storro

cmake_minimum_required (VERSION 3.8)
project ("HashPumpWIN32")

# NOTE: Set following system environment variables:
# -> OPENSSL_ROOT_DIR       to OpenSSL Win32 build path (see README)
# -> PYTHON36_ROOT_DIR      to Python 3.6 path

# WARNING: this will work ONLY on Windows

set(OpenSSL_INCLUDE_DIR     $ENV{OPENSSL_ROOT_DIR}/include)
set(OpenSSL_LIB_DIR         $ENV{OPENSSL_ROOT_DIR}/lib)
set(OpenSSL_LIBS            ${OpenSSL_LIB_DIR}/libcrypto.lib
                            ${OpenSSL_LIB_DIR}/libssl.lib)

set(PYTHON36_INCLUDE_DIR     $ENV{PYTHON36_ROOT_DIR}/include)
set(PYTHON36_LIB_DIR         $ENV{PYTHON36_ROOT_DIR}/libs)
set(PYTHON36_LIBS            ${PYTHON36_LIB_DIR}/python36_d.lib)

include_directories(${OpenSSL_INCLUDE_DIR} ${PYTHON36_INCLUDE_DIR})
link_directories(${OpenSSL_LIB_DIR} ${PYTHON36_LIB_DIR})

set(HEADERS
	./CRC32ex.h
    ./Extender.h
    ./getopt.h
    ./MD4ex.h
    ./MD5ex.h
    ./SHA1.h
    ./SHA256.h
    ./SHA512ex.h
    ./unistd.h
)
 
set(SOURCES
    ./CRC32ex.cpp
    ./Extender.cpp
    ./getopt.c
    ./hashpumpy.cpp
    ./main.cpp
    ./MD4ex.cpp
    ./MD5ex.cpp
    ./SHA1.cpp
    ./SHA256.cpp
    ./SHA512ex.cpp
)

add_executable (HashPumpWIN32 ${HEADERS} ${SOURCES})
target_link_libraries(HashPumpWIN32 ${OpenSSL_LIBS} ${PYTHON36_LIBS})
