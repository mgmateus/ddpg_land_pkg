cmake_minimum_required(VERSION 3.0.2)
project(ddpg_land_pkg)

# todo eigen3 in AirLib already
find_package(catkin REQUIRED COMPONENTS
  cv_bridge
  image_transport
  mavros_msgs
  message_generation
  nav_msgs
  # nodelet
  roscpp
  rospy
  sensor_msgs
  std_msgs
  std_srvs
  tf2
  tf2_ros
)

add_message_files(
  FILES
  ProcessedImg.msg
)

generate_messages(
  DEPENDENCIES
  std_msgs
)

catkin_package(
  INCLUDE_DIRS
  CATKIN_DEPENDS message_runtime roscpp std_msgs  airsim_ros_pkgs
)



include_directories(
  ${catkin_INCLUDE_DIRS}
  ${airsim_ros_pkgs_INCLUDE_DIRS}
)

find_package( OpenCV REQUIRED )

add_executable(vision_node src/vision.cpp src/main.cpp)
target_link_libraries(vision_node ${catkin_LIBRARIES} ${OpenCV_LIBRARIES})
