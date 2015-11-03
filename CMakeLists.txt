cmake_minimum_required (VERSION 2.8)
project (tabixpp)

# C++11
set (CMAKE_CXX_FLAGS "-W -Wall -Wfatal-errors -pedantic -Wno-variadic-macros -lrt -O3 -std=c++11 -DSEQAN_HAS_ZLIB=1 -DNDEBUG -DSEQAN_ENABLE_TESTING=0 -DSEQAN_ENABLE_DEBUG=0")

# Set module path
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/utilities")

include_directories("${PROJECT_BINARY_DIR}")

# Find external libraries
message (STATUS "Checking for zlib")
find_package(ZLIB REQUIRED)
include_directories( ${ZLIB_INCLUDE_DIRS} )

# Find htslib (libfind_package(HTSlib))
# find_package(htslib REQUIRED)

add_subdirectory(utilities/htslib)
message("${htslib_INCLUDE_DIRS}")
include_directories(${htslib_INCLUDE_DIRS})


set(EXECUTABLE_OUTPUT_PATH ../bin)
add_subdirectory(src)
