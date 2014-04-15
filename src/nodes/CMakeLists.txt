# common source files for both node and nodelet driver interfaces
set(DRIVER_SOURCES 
  driver1394.cpp
  dev_camera1394.cpp
  features.cpp
  format7.cpp
  modes.cpp)

# Mac OSX requires extra linker parameters
if(CMAKE_SYSTEM_NAME MATCHES "Darwin")
  set(DC1394 dc1394 "-framework CoreServices")
else(CMAKE_SYSTEM_NAME MATCHES "Darwin")
  set(DC1394 dc1394)
endif(CMAKE_SYSTEM_NAME MATCHES "Darwin")

add_executable(camera1394_node camera1394_node.cpp ${DRIVER_SOURCES})
target_link_libraries(camera1394_node ${catkin_LIBRARIES} ${DC1394})
add_dependencies(camera1394_node ${PROJECT_NAME}_gencfg)

add_library(camera1394_nodelet nodelet.cpp ${DRIVER_SOURCES})
target_link_libraries(camera1394_nodelet ${catkin_LIBARIES} ${DC1394})
add_dependencies(camera1394_nodelet ${PROJECT_NAME}_gencfg)

install(TARGETS camera1394_node
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(TARGETS camera1394_nodelet
  DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
)
