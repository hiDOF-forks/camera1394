cmake_minimum_required(VERSION 2.4.6)
project(camera1394)

find_package(catkin REQUIRED
  COMPONENTS
    roscpp
    diagnostic_updater
    dynamic_reconfigure
    driver_base
    tf
    camera_info_manager
    image_transport
    nodelet
    roslib
    rostest
)

# auto-generated dynamic reconfiguration GUI
generate_dynamic_reconfigure_options(
  cfg/Camera1394.cfg
)

catkin_package(
  INCLUDE_DIRS 
  LIBRARIES camera1394_nodelet
  CATKIN_DEPENDS diagnostic_updater dynamic_reconfigure driver_base tf camera_info_manager image_transport nodelet roscpp roslib rostest
  DEPENDS
)

include_directories(${catkin_INCLUDE_DIRS})

# build package sources
add_subdirectory(src/nodes)

# driver unit tests
if (CATKIN_ENABLE_TESTING)
  add_rostest(tests/no_device_node.test)
  add_rostest(tests/no_device_nodelet.test)
  if(${device})
    add_rostest(tests/camera_node_hz.test)
    add_rostest(tests/camera_nodelet_hz.test)
  endif()
endif()
