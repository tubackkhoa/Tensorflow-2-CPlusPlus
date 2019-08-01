cmake_minimum_required(VERSION 3.7)
project(tf_detector_example)

set(CMAKE_CXX_STANDARD 11)

if(NOT DEFINED HEADERS)
    file(GLOB HEADERS ${CMAKE_CURRENT_SOURCE_DIR}/*.h)
endif()

if(NOT DEFINED SOURCES)
    file(GLOB SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp)
endif()

# OpenCV libs
find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})

# ==================== PATHS TO SPECIFY! ==================== #

# Eigen lib headers
include_directories("/usr/local/include/eigen3")

# TensorFlow headers
include_directories("/usr/local/include")
include_directories("/usr/local/include/tf/")
include_directories("/usr/local/include/tf/bazel-genfiles/")
include_directories("/usr/local/include/tf/tensorflow/")
include_directories("/usr/local/include/tf/third-party/")

if(APPLE)    
    set(TENSORFLOW_FRAMEWORK "/usr/local/lib/libtensorflow_framework.dylib")      
else()
    set(TENSORFLOW_FRAMEWORK "/usr/local/lib/libtensorflow_framework.so")
endif()

macro(build_project name)

  add_executable(${name} ${HEADERS} ${SOURCES})

  # Link TensorFlow libs
  target_link_libraries(${name} 
    ${OpenCV_LIBS}  
    ${TENSORFLOW_FRAMEWORK}
    "/usr/local/lib/libtensorflow_cc.so"
  )
endmacro()

build_project(${PROJECT_NAME})