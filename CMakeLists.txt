CMAKE_MINIMUM_REQUIRED(VERSION 2.8.5 FATAL_ERROR)
PROJECT(hphp C CXX ASM)

set(HHVM_DEFINITIONS ";ENABLE_ZEND_COMPAT=1;HHVM_DYNAMIC_EXTENSION_DIR=\"/usr/local/lib/x86_64-linux-gnu/hhvm/extensions\";HAVE_LIBDL;HAVE_BOOST1_49;HAVE_FEATURES_H=1;HAVE_CURL_MULTI_WAIT;USE_JEMALLOC=1;NO_TCMALLOC=1;USE_EDITLINE;LIBDWARF_USE_INIT_C;HAVE_ELF_GETSHDRSTRNDX;FOLLY_HAVE_WEAK_SYMBOLS=1;_REENTRANT=1;_PTHREADS=1;__STDC_FORMAT_MACROS;_GNU_SOURCE;RELEASE=1;NDEBUG;ENABLE_FASTCGI=1;HPHP_OSS=1;PACKAGE=hhvm;PACKAGE_VERSION=Release;FOLLY_NO_CONFIG=1;FOLLY_HAVE_CLOCK_GETTIME=1;FOLLY_HAVE_FEATURES_H=1;HHVM;USE_CMAKE")
set(HHVM_API_VERSION "20140829")
set(CMAKE_INSTALL_PREFIX "/usr/local")
set(CMAKE_INSTALL_LIBDIR "lib/x86_64-linux-gnu")
set(CMAKE_BUILD_TYPE "Release")
set(ENABLE_ZEND_COMPAT "ON")

option(HHVM_DSO_TEST_MODE "Build against source headers, not installed ones" Off)
if (HHVM_DSO_TEST_MODE)
  set(HHVM_INCLUDE_DIRS "/usr/include;/usr/include;/usr/include;/usr/include/x86_64-linux-gnu;/usr/include;/usr/include/mysql;/usr/include/mysql;/usr/include;/usr/local/include;/usr/include;/usr/include;/usr/include/libxml2;/usr/include;/usr/include;/usr/include/double-conversion;/usr/include;/usr/include;/usr/lib/x86_64-linux-gnu/libzip/include;/usr/include/x86_64-linux-gnu;/usr/include;/usr/include;/usr/include;/usr/include;/usr/include;/usr/include;/usr/include;/usr/include;/usr/include;/usr/include;/usr/include;/usr/include;/usr/include/security;/home/longlong/hhvm/hphp;/home/longlong/hhvm/third-party/fastlz;/home/longlong/hhvm/third-party/timelib;/home/longlong/hhvm/third-party/libafdt/src;/home/longlong/hhvm/third-party/libmbfl;/home/longlong/hhvm/third-party/libmbfl/mbfl;/home/longlong/hhvm/third-party/libmbfl/filter;/home/longlong/hhvm/third-party/folly;/home/longlong/hhvm/third-party;/home/longlong/hhvm/hphp;/home/longlong/hhvm;/usr/include")
  set(CMAKE_MODULE_PATH
    ${CMAKE_CURRENT_SOURCE_DIR}
    "/home/longlong/hhvm/CMake" "/home/longlong/hhvm/hphp/public_tld/CMake"
    ${CMAKE_MODULE_PATH})
else()
  set(HHVM_INCLUDE_DIRS "/usr/local/include;/usr/include;/usr/include;/usr/include;/usr/include/x86_64-linux-gnu;/usr/include;/usr/include/mysql;/usr/include/mysql;/usr/include;/usr/local/include;/usr/include;/usr/include;/usr/include/libxml2;/usr/include;/usr/include;/usr/include/double-conversion;/usr/include;/usr/include;/usr/lib/x86_64-linux-gnu/libzip/include;/usr/include/x86_64-linux-gnu;/usr/include;/usr/include;/usr/include;/usr/include;/usr/include;/usr/include;/usr/include;/usr/include;/usr/include;/usr/include;/usr/include;/usr/include;/usr/include/security;/usr/local/include/hphp;/usr/local/include/hphp/third-party/fastlz;/usr/local/include/hphp/third-party/timelib;/usr/local/include/hphp/third-party/libafdt/src;/usr/local/include/hphp/third-party/libmbfl;/usr/local/include/hphp/third-party/libmbfl/mbfl;/usr/local/include/hphp/third-party/libmbfl/filter;/usr/local/include/hphp/third-party;/usr/local/include/hphp;/usr/include")
  set(CMAKE_MODULE_PATH
    ${CMAKE_CURRENT_SOURCE_DIR}
    "${CMAKE_INSTALL_PREFIX}/${CMAKE_INSTALL_LIBDIR}/hhvm/CMake"
    ${CMAKE_MODULE_PATH})
endif()

message(STATUS "Configuring for HHVM API version ${HHVM_API_VERSION}")

include(HPHPFunctions)
include(HPHPIZEFunctions)
include(HPHPCompiler)
include(config)

foreach (dir ${HHVM_INCLUDE_DIRS})
  include_directories(${dir})
endforeach()

add_definitions("-DHHVM_BUILD_DSO")
foreach (def ${HHVM_DEFINITIONS})
  add_definitions("-D${def}")
endforeach()
