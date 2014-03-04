#		cmake_minimum_required(VERSION 2.6)
#		include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)
#
#		# Set the build type.  Options are:
#		#  Coverage       : w/ debug symbols, w/o optimization, w/ code-coverage
#		#  Debug          : w/ debug symbols, w/o optimization
#		#  Release        : w/o debug symbols, w/ optimization
#		#  RelWithDebInfo : w/ debug symbols, w/ optimization
#		#  MinSizeRel     : w/o debug symbols, w/ optimization, stripped binaries
#		#set(ROS_BUILD_TYPE RelWithDebInfo)
#
#		rosbuild_init()
#
#		#set the default path for built executables to the "bin" directory
#		set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#		#set the default path for built libraries to the "lib" directory
#		set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)
#
#		#uncomment if you have defined messages
#		#genmsg()
#		#rosbuild_genmsg()
#		#uncomment if you have defined services
#		#gensrv()
#
#		#common commands for building c++ executables and libraries
#		#rospack_add_library(${PROJECT_NAME} src/example.cpp)
#		#target_link_libraries(${PROJECT_NAME} another_library)
#		#rospack_add_boost_directories()
#		#rospack_link_boost(${PROJECT_NAME} thread)
#		#rospack_add_executable(example examples/example.cpp)
#		#target_link_libraries(example ${PROJECT_NAME})
#
#		rosbuild_add_executable(ros_vrpn_client src/ros_vrpn_client.cpp)
#		target_link_libraries(ros_vrpn_client vrpn)
#		#target_link_libraries(vrpn ${PROJECT_SOURCE_DIR}/vrpn/pc_linux)

cmake_minimum_required(VERSION 2.8.3)
project(ros_vrpn_client)

find_package(catkin REQUIRED COMPONENTS roscpp tf geometry_msgs)

catkin_package(
	INCLUDE_DIRS vrpn
)

include_directories(vrpn)
include_directories(
	${catkin_INCLUDE_DIRS}
)

add_executable(ros_vrpn_client src/ros_vrpn_client.cpp 
	vrpn/vrpn_Connection.C vrpn/vrpn_Tracker.C vrpn/vrpn_Shared.C vrpn/vrpn_FileConnection.C
	vrpn/vrpn_BaseClass.C vrpn/vrpn_Serial.C)
target_link_libraries(ros_vrpn_client ${catkin_LIBRARIES})
