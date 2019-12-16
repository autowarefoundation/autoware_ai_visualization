cmake_minimum_required(VERSION 2.8.3)
project(fastvirtualscan)

find_package(autoware_build_flags REQUIRED)
find_package(catkin REQUIRED COMPONENTS
  roscpp
  sensor_msgs
)

find_package(Qt5Core REQUIRED)

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES fastvirtualscan
)

SET(CMAKE_CXX_FLAGS "-O2 -g -Wall ${CMAKE_CXX_FLAGS}")

include_directories(
  include
  ${catkin_INCLUDE_DIRS}
  ${Qt5Core_INCLUDE_DIRS}
)

add_library(fastvirtualscan
  FastVirtualScan/fastvirtualscan.cpp
)

target_link_libraries(fastvirtualscan
  Qt5::Core
  ${catkin_LIBRARIES}
)

install(
  DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.h"
)

install(TARGETS fastvirtualscan
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
