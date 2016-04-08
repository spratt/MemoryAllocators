cmake_minimum_required (VERSION 3.4)

project (MemoryAllocators)

set (MemoryAllocators_VERSION_MAJOR 1)
set (MemoryAllocators_VERSION_MINOR 0)

find_package(Boost 1.59)

if(${Boost_FOUND})
    add_library(boost INTERFACE IMPORTED)
    set_property(TARGET boost PROPERTY INTERFACE_INCLUDE_DIRECTORIES ${Boost_INCLUDE_DIR})
endif()

add_executable(bsd_allocator bsd_allocator.cpp)
add_executable(indiana_allocator indiana_allocator.cpp)
add_executable(linux_buddy_system linux_buddy_system.cpp)

target_link_libraries(bsd_allocator boost)
target_link_libraries(indiana_allocator boost)
target_link_libraries(linux_buddy_system boost)

set_target_properties(bsd_allocator PROPERTIES CXX_STANDARD 11)
set_target_properties(indiana_allocator PROPERTIES CXX_STANDARD 11)
set_target_properties(linux_buddy_system PROPERTIES CXX_STANDARD 11)

add_custom_target(runbsd
  COMMAND bsd_allocator
)
add_custom_target(runind
  COMMAND indiana_allocator
)
add_custom_target(runlin
  COMMAND linux_buddy_system
)
