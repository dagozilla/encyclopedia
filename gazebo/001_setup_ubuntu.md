# Gazebo Installation for Ubuntu

## Default installation: one-liner
1. Install
```sh
curl -sSL http://get.gazebosim.org | sh
```
2. Run
```sh
gazebo
```

## Run Gazebo
The `gazebo` command actually runs two different executables for you. The first is called `gzserver`, and the second `gzclient`.

The `gzserver` executable runs the physics update-loop and sensor data generation. This is the core of Gazebo, and can be used independently of a graphical interface. An example use case would involve running `gzserver` on a cloud computer where a user interface is not needed.

The `gzclient` executable runs a QT based user interface. This application provides a nice visualization of simulation, and convenient controls over various simulation properties.

## Install Gazebo Plugin & Gazebo ROS
```sh
# install gazebo plugin (replace 11 with your gazebo version)
sudo apt install libgazebo11-dev

# install gazebo ros
sudo apt install ros-noetic-gazebo-ros-pkgs ros-noetic-gazebo-ros-control
```

## Refence
1. ["Gazebo: Tutorial: Ubuntu"](http://gazebosim.org/tutorials?tut=install_ubuntu&cat=install). *gazbosim.org*. Retrieved 20 June 2021
2. ["Gazebo: Tutorial: Quick Start"](http://gazebosim.org/tutorials?tut=quick_start&cat=get_started). *gazbosim.org*. Retrieved 20 June 2021
3. ["Gazebo: Tutorial: Plugins 101"](http://gazebosim.org/tutorials?tut=plugins_hello_world&cat=write_plugin). *gazbosim.org*. Retrieved 21 June 2021
4. ["Gazebo: Tutorial: Installing gazebo_ros_pkgs (ROS 1)"](http://gazebosim.org/tutorials?tut=ros_installing&cat=connect_ros). *gazbosim.org*. Retrieved 21 June 2021