cmake_minimum_required(VERSION 2.8.3)
project(caliberate)

find_package(catkin REQUIRED COMPONENTS
  cv_bridge 
  image_geometry
  roscpp
  rospy
  std_msgs
  geometry_msgs
  image_transport
  message_generation
)

generate_messages(
   DEPENDENCIES
   std_msgs
   geometry_msgs
)

include_directories(include ${catkin_INCLUDE_DIRS} ${OpenCV_INCLUDE_DIRS})
find_package(OpenCV REQUIRED)
catkin_package(
  LIBRARIES caliberate
  CATKIN_DEPENDS message_runtime nodelet cv_bridge roscpp std_msgs geometry_msgs 
)
add_executable(Imgpub src/Imgpub.cpp)

target_link_libraries(Imgpub ${catkin_LIBRARIES} ${OpenCV_LIBS})
add_dependencies(Imgpub ros_calibrate_generate_messages_cpp)

