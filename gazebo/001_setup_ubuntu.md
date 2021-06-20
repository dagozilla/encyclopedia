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

## Refence
1. ["Gazebo: Tutorial: Ubuntu"](http://gazebosim.org/tutorials?tut=install_ubuntu&cat=install). *gazbosim.org*. Retrieved 20 June 2021
2. ["Gazebo: Tutorial: Quick Start"](http://gazebosim.org/tutorials?tut=quick_start&cat=get_started). *gazbosim.org*. Retrieved 20 June 2021