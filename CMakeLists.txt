cmake_minimum_required(VERSION 3.23)
project(LibTest VERSION 1.0)

if (MSVC)
    set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON)
endif()

add_library(DynLib SHARED)
target_include_directories(DynLib PRIVATE "${PROJECT_SOURCE_DIR}")
add_subdirectory("DynLib")

add_executable(libtest)
target_sources(libtest PRIVATE "LibTest/LibTest.cpp")
target_link_libraries(libtest PRIVATE DynLib)

install(TARGETS DynLib
        # for executables and dll on Win
        RUNTIME DESTINATION bin
        # shared libraries
        LIBRARY DESTINATION lib
        # for static libraries
        ARCHIVE DESTINATION lib
        INCLUDES DESTINATION include)