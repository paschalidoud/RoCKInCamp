cmake_minimum_required(VERSION 2.8.3)
project(object_recognition)

find_package(catkin REQUIRED COMPONENTS roscpp 
										sensor_msgs 
										std_msgs 
										cv_bridge 
										rec_msg_and_serv
										tf )

find_package(Qt4 REQUIRED)
find_package(OpenCV REQUIRED)

catkin_package(
    DEPENDS 
    CATKIN-DEPENDS 
    INCLUDE_DIRS 
    LIBRARIES 
)

include_directories(${OPENCV_INCLUDE_DIRS})
link_directories(${OPENCV_LIBRARY_DIRS})


set(QT_USE_QTOPENGL TRUE)
include(${QT_USE_FILE})

add_definitions(${QT_DEFINITIONS})
add_definitions(-Dlinux -D__x86_64__)

include_directories(${QT_INCLUDE_DIR})
include_directories(${QT_INCLUDE_DIR}/QtOpenGL)

message(STATUS "QT_INCLUDE_DIR: ${QT_INCLUDE_DIR}")
message(STATUS "QT_USE_FILE: ${QT_USE_FILE}")
message(STATUS "QT_DEFINITIONS: ${QT_DEFINITIONS}")
message(STATUS "QT_LIBRARIES: ${QT_LIBRARIES}")

message(STATUS "OPENCV_LIBRARIES: ${OPENCV_LIBRARIES}")



catkin_package(
   INCLUDE_DIRS include

)


include_directories(include
  ${catkin_INCLUDE_DIRS}
)


################################rec_node########################
add_executable(rec_node src/rec/rec_node.cpp 
                   src/rec/recognizer.cpp)
  set(TRACKER_QT_LIBRARIES v4rTracker v4rTomGine v4rTomGineIP v4rRecognizer3D)

  target_link_libraries(rec_node
      ${catkin_LIBRARIES}
      ${OPENCV_LIBRARIES} opencv_core opencv_highgui
      ${QT_LIBRARIES}
      ${TRACKER_QT_LIBRARIES}
    )
    
#####################rec_test_node##############################
add_executable(rec_test_node src/rec_test/main.cpp)

  target_link_libraries(rec_test_node
      ${catkin_LIBRARIES}
    )
  
  
