cmake_minimum_required(VERSION 3.4)
project(cmake_wrapper)

include(conanbuildinfo.cmake)
conan_basic_setup(KEEP_RPATHS)

if(MSVC)
    if(MSVC_VERSION LESS 1900)
      add_definitions(-DMBEDTLS_PLATFORM_SNPRINTF_MACRO=MBEDTLS_PLATFORM_STD_SNPRINTF)
    else()
      add_definitions(-DMBEDTLS_PLATFORM_SNPRINTF_MACRO=snprintf)
    endif()
    if(BUILD_SHARED_LIBS)
        add_definitions(-DX509_BUILD_SHARED)
        set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON)
    endif()
endif()

add_subdirectory(source_subfolder)
