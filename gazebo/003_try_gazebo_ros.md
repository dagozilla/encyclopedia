# Gazebo ROS Example

1. Create package
```sh
catkin_create_pkg simulator_gazebo
```

2. Edit CMakeList
```cmake
cmake_minimum_required(VERSION 2.8.3)
project(simulator_gazebo)

find_package(catkin REQUIRED COMPONENTS
  gazebo_ros
)

# Depend on system install of Gazebo
find_package(gazebo REQUIRED)

include_directories(include ${catkin_INCLUDE_DIRS} ${GAZEBO_INCLUDE_DIRS} ${SDFormat_INCLUDE_DIRS})

# Build whatever you need here
add_library(...) # TODO

catkin_package(
    DEPENDS
      gazebo_ros
    CATKIN_DEPENDS
    INCLUDE_DIRS
    LIBRARIES
)
```

3. Add dependency in package.xml
```xml
<buildtool_depend>gazebo_ros</buildtool_depend>
<exec_depend>gazebo_ros</exec_depend>
```