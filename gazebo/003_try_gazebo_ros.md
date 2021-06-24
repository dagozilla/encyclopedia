# Gazebo ROS Example

1. Create package. Firstly make the workspace `~/tutorial_gazebo_ws` for example and make `src` directory. Then create the package in `src` directory
```sh
catkin_create_pkg tutorial_gazebo
```

2. Edit `CMakeLists.txt`
```cmake
cmake_minimum_required(VERSION 2.8.3)
project(tutorial_gazebo)

find_package(catkin REQUIRED COMPONENTS
  gazebo_ros
)

# Depend on system install of Gazebo
find_package(gazebo REQUIRED)

include_directories(include ${catkin_INCLUDE_DIRS} ${GAZEBO_INCLUDE_DIRS} ${SDFormat_INCLUDE_DIRS})

# Build whatever you need here
# add_library(...) # TODO
add_library(model_push SHARED plugin/model_push.cc)
target_link_libraries(model_push ${GAZEBO_LIBRARIES})

catkin_package(
    DEPENDS
      gazebo_ros
    CATKIN_DEPENDS
    INCLUDE_DIRS
    LIBRARIES
)
```

3. Add dependency in `package.xml`
```xml
<buildtool_depend>gazebo_ros</buildtool_depend>
<exec_depend>gazebo_ros</exec_depend>
```

4. Copy the previous `models` and `worlds` directory to `~/tutorial_gazebo_ws/src/tutorial_gazebo/`

5. Copy `model_push.cc` to `tutorial_gazebo/plugin/model_push.cc`

6. Add in the `CMakeLists.txt`
add_library(model_push SHARED plugin/model_push.cc)
target_link_libraries(model_push ${GAZEBO_LIBRARIES})

7. Make the launch file. For example `my_launch.launch`:
```xml
<launch>
  <include file="$(find gazebo_ros)/launch/empty_world.launch">
    <arg name="world_name" value="$(find tutorial_gazebo)/worlds/world.world"/>
    <arg name="paused" value="true"/>
    <arg name="use_sim_time" value="true"/>
    <arg name="gui" value="true"/>
    <arg name="recording" value="false"/>
    <arg name="debug" value="false"/>
  </include>

  <node 
    name="spawn_sdf" 
    pkg="gazebo_ros"
    type="spawn_model"
    args="-file $(find tutorial_gazebo)/models/my_robot/model.sdf -sdf -model my_robot1" />
</launch>
```

8. Do command at `~/tutorial_gazebo_ws`:
```sh
catkin_make
source devel/setup.bash
roslaunch tutorial_gazebo my_launch.launch
```

## References
1. ["Gazebo: Tutorial: ROS overview"](http://gazebosim.org/tutorials?tut=ros_overview&cat=connect_ros). *gazbosim.org*. Retrieved 22 June 2021
2. ["Gazebo: Tutorial: Using roslaunch"](http://gazebosim.org/tutorials?tut=ros_roslaunch&cat=connect_ros). *gazbosim.org*. Retrieved 23 June 2021