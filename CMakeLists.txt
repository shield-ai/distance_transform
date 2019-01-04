cmake_minimum_required(VERSION 3.3)

project(distance_transform)

find_package(catkin REQUIRED)

catkin_package(
 LIBRARIES distance_transform
 INCLUDE_DIRS include
)

set(CMAKE_CXX_STANDARD 14)

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/extern/DopeVector ${CMAKE_CURRENT_BINARY_DIR}/lib_dope_vector)
include(${CMAKE_CURRENT_SOURCE_DIR}/extern/DopeVector/sources_properties.cmake)

set(toLink DopeVector)
if(CMAKE_COMPILER_IS_GNUCXX)
	find_package(Threads REQUIRED)
	list(APPEND toLink Threads::Threads)
endif()

set(hdr_dir ${CMAKE_CURRENT_SOURCE_DIR}/include)

add_library(${PROJECT_NAME} INTERFACE)

target_include_directories(${PROJECT_NAME} INTERFACE ${hdr_dir})
target_link_libraries(${PROJECT_NAME} INTERFACE ${toLink})

install(TARGETS distance_transform
        ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
        LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
        RUNTIME DESTINATION ${CATKIN_GLOBAL_BIN_DESTINATION})

# Install headers.
install(DIRECTORY distance_transform
  DESTINATION ${CATKIN_GLOBAL_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.hpp"
)
