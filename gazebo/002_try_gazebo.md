# Try Gazebo

## Try Model and World
1. Create a directory. For example:
```sh
mkdir ~/gazebo_tutorial
cd ~/gazebo_tutorial
```

2. Create a model. You can copy from [example/models/my_robot](example/models/my_robot) to `~/gazebo_tutorial/models/my_robot`

3. Open Gazebo
```sh
# -u to launch gazebo in pause state
gazebo -u
```

4. Insert the model you've created. You can add `~/gazebo_tutorial/models` path first at the insert tab and then insert the model.

5. You can then save the world for example to `~/gazebo_tutorial/worlds/my_world.world`. If you run gazebo with:
```sh
gazebo -u ~/gazebo_tutorial/worlds/my_world.world
```
you will see the world with the model you've created previously.


## Try Plugin
1. Make sure you're at `~/gazebo_tutorial`

2. Create a plugin. You can copy from [example/model_push.cc](example/model_push.cc) to `~/gazebo_tutorial/model_push.cc`

3. Then, copy the [CMakeLists.txt](example/CMakeLists.txt) to `~/gazebo_tutorialCMakeLists.txt`

4. Compile the plugin
```sh
mkdir build
cd build
cmake ../
make
```

5. Add the plugin to a model. You can use [example/worlds/model_push.world](example/worlds/model_push.world) that has the model wtih the plugin.

6. Add the plugin path
```sh
export GAZEBO_PLUGIN_PATH=$HOME/gazebo_tutorial/build:$GAZEBO_PLUGIN_PATH
```

7. Run gazebo
```sh
gazebo ~/gazebo_tutorial/worlds/model_push.world
```
You will see that the box model is moving.

## References
1. ["Gazebo: Tutorial: Make a Mobile Robot"](http://gazebosim.org/tutorials?tut=build_robot&cat=build_robot). *gazbosim.org*. Retrieved 22 June 2021
2. ["Gazebo: Tutorial: Model plugins"](http://gazebosim.org/tutorials?tut=plugins_model&cat=write_plugin). *gazbosim.org*. Retrieved 22 June 2021
