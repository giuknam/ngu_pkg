cmake_minimum_required(VERSION 3.0.2)
project(ngu_pkg)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
  message_generation
)

add_message_files(
  FILES
  test_msg.msg
)

generate_messages(
  DEPENDENCIES
  std_msgs
)

catkin_package(
  LIBRARIES test_pkg
  CATKIN_DEPENDS roscpp rospy std_msgs message_runtime
)

include_directories(
  include
  ${catkin_INCLUDE_DIRS}
)

add_executable(hello_world_pubnode src/hello_world_pubnode.cpp)
add_executable(hello_world_subnode src/hello_world_subnode.cpp)

target_link_libraries(hello_world_pubnode
  ${catkin_LIBRARIES}
)
target_link_libraries(hello_world_subnode
  ${catkin_LIBRARIES}
)

catkin_install_python(PROGRAMS
  src/hello_pub.py
  src/hello_sub.py
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
