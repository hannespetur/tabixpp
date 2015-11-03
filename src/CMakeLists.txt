cmake_minimum_required(VERSION 2.8)

# Create a fastahack library
set(tabix_SOURCE_FILES
    tabix.cpp
)

add_library(tabix_core ${tabix_SOURCE_FILES})
include_directories(${CMAKE_CURRENT_SOURCE_DIR})

add_executable(tabix main.cpp)
target_link_libraries(tabix tabix_core ${HTSlib_LIBRARY} ${ZLIB_LIBRARIES})

# Add the executable
target_link_libraries(tabix ${LIBS})

# Installs tabix to /usr/local/bin using [sudo] make install
install (TARGETS tabix DESTINATION bin)
