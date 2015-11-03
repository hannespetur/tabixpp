cmake_minimum_required(VERSION 2.8)
message("Fetching htslib from Github")
project(htslib_builder CXX)
include(ExternalProject)
find_package(Git REQUIRED)

ExternalProject_Add(
    htslib
    PREFIX ${CMAKE_BINARY_DIR}/htslib
    GIT_REPOSITORY https://github.com/samtools/htslib.git
    GIT_TAG develop
    TIMEOUT 30
    UPDATE_COMMAND ${GIT_EXECUTABLE} pull origin develop
    CONFIGURE_COMMAND ""
    BUILD_COMMAND $(MAKE) -C ${CMAKE_BINARY_DIR}/htslib/src/htslib
    INSTALL_COMMAND ""
    LOG_DOWNLOAD ON
   )

# Expose required variable (SEQAN_INCLUDE_PATH) to parent scope
ExternalProject_Get_Property(htslib source_dir)
set(htslib_INCLUDE_DIRS ${source_dir} CACHE INTERNAL "Path to include folder for htslib")
set(HTSlib_LIBRARY ${source_dir}/libhts.so CACHE INTERNAL "Path to library folder for htslib")
