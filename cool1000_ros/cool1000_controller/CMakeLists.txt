cmake_minimum_required(VERSION 2.8.3)
project(cool1000_controller)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages

# Load catkin and all dependencies required for this package
find_package(catkin REQUIRED COMPONENTS 
  roscpp 
  rospy 
  std_msgs
  actionlib
  cool1000_msgs
  dynamixel_msgs
  sensor_msgs
  tf
)

# Declare a catkin package
catkin_package(
  CATKIN_DEPENDS 
    roscpp 
    rospy 
    std_msgs
    actionlib 
    std_msgs 
    sensor_msgs
    dynamixel_msgs
    tf
#  INCLUDE_DIRS include
#  LIBRARIES ${PROJECT_NAME}
)

## Build 
include_directories(
  include 
  ${catkin_INCLUDE_DIRS}
)

# ---------------
add_executable(joint_state_aggregator src/joint_state_aggregator.cpp)
target_link_libraries(joint_state_aggregator ${catkin_LIBRARIES} )

# ---------------
add_executable(cool1000_gripper_controller src/cool1000_gripper_controller.cpp)
add_dependencies(cool1000_gripper_controller cool1000_msgs_gencpp ${PROJECT_NAME}_gencfg) # wait for clam_msgs to be built
target_link_libraries(cool1000_gripper_controller ${catkin_LIBRARIES})
## System dependencies are found with CMake's conventions
# find_package(Boost REQUIRED COMPONENTS system)
#------------------------------------------
add_executable(cool1000_gripper_controller_test src/cool1000_gripper_controller_test.cpp)
add_dependencies(cool1000_gripper_controller_test cool1000_msgs_gencpp ${PROJECT_NAME}_gencfg) # wait for clam_msgs to be built
target_link_libraries(cool1000_gripper_controller_test ${catkin_LIBRARIES})
#------------------------------------------
## Uncomment this if the package has a setup.py. This macro ensures
## modules and global scripts declared therein get installed
## See http://ros.org/doc/api/catkin/html/user_guide/setup_dot_py.html
# catkin_python_setup()

#######################################
## Declare ROS messages and services ##
#######################################



## Generate messages in the 'msg' folder
# add_message_files(
#   FILES
#   Message1.msg
#   Message2.msg
# )

## Generate services in the 'srv' folder
# add_service_files(
#   FILES
#   Service1.srv
#   Service2.srv
# )

## Generate added messages and services with any dependencies listed here
# generate_messages(
#   DEPENDENCIES
#   std_msgs  # Or other packages containing msgs
# )

###################################
## catkin specific configuration ##
###################################
## The catkin_package macro generates cmake config files for your package
## Declare things to be passed to dependent projects
## INCLUDE_DIRS: uncomment this if you package contains header files
## LIBRARIES: libraries you create in this project that dependent projects also need
## CATKIN_DEPENDS: catkin_packages dependent projects also need
## DEPENDS: system dependencies of this project that dependent projects also need


###########
## Build ##
###########

## Specify additional locations of header files
## Your package locations should be listed before other locations
# include_directories(include)

## Declare a cpp library
# add_library(elite_controller
#   src/${PROJECT_NAME}/elite_controller.cpp
# )

## Declare a cpp executable
# add_executable(elite_controller_node src/elite_controller_node.cpp)

## Add cmake target dependencies of the executable/library
## as an example, message headers may need to be generated before nodes
# add_dependencies(elite_controller_node elite_controller_generate_messages_cpp)

## Specify libraries to link a library or executable target against
# target_link_libraries(elite_controller_node
#   ${catkin_LIBRARIES}
# )



#############
## Install ##
#############

# all install targets should use catkin DESTINATION variables
# See http://ros.org/doc/api/catkin/html/adv_user_guide/variables.html

## Mark executable scripts (Python etc.) for installation
## in contrast to setup.py, you can choose the destination
# install(PROGRAMS
#   scripts/my_python_script
#   DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

## Mark executables and/or libraries for installation
# install(TARGETS elite_controller elite_controller_node
#   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

## Mark cpp header files for installation
# install(DIRECTORY include/${PROJECT_NAME}/
#   DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
#   FILES_MATCHING PATTERN "*.h"
#   PATTERN ".svn" EXCLUDE
# )

## Mark other files for installation (e.g. launch and bag files, etc.)
# install(FILES
#   # myfile1
#   # myfile2
#   DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
# )

#############
## Testing ##
#############

## Add gtest based cpp test target and link libraries
# catkin_add_gtest(${PROJECT_NAME}-test test/test_elite_controller.cpp)
# if(TARGET ${PROJECT_NAME}-test)
#   target_link_libraries(${PROJECT_NAME}-test ${PROJECT_NAME})
# endif()

## Add folders to be run by python nosetests
# catkin_add_nosetests(test)
