cmake_minimum_required(VERSION 2.8.3)
project(test_one)

add_compile_options(-std=c++14)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  sensor_msgs
)


catkin_package(
  INCLUDE_DIRS include
  CATKIN_DEPENDS roscpp sensor_msgs
)



find_package(Boost REQUIRED)
include_directories(include
  ${catkin_INCLUDE_DIRS}
  ${Boost_INCLUDES}
)

find_package(GTest REQUIRED)
include_directories(${GTEST_INCLUDE_DIRS})

add_executable(test_one src/test_one.cpp)
target_link_libraries(test_one ${catkin_LIBRARIES})

#Link runTests with what we want to test and the GTest and pthread library
add_executable(runTests src/tests.cpp)
target_link_libraries(runTests ${GTEST_LIBRARIES} pthread)
