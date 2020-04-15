# Crazyballoon
Crazyflie modification to airship using balloon. Mainly Instructions on Installation &amp; Usage.

# Mechanics and Electronics #

Design files for both ECAD &amp; MCAD can be found on this <a href="https://github.com/tau-adl/crazybal-design-files"> repository </a>.
Assembly and more can be found in the final project paper in this repo

# Crazyfile Firmware #

In order to fly the airship, a modified version of the firmware is needed.

## Instructions ##

The modified firmware, along with enviroment setup can be found on this <a href="https://github.com/tau-adl/crazyfile-firmware.git"> repository </a>.</br>
For some python utility scripts (and for cfclient) it is required to install <a href="https://github.com/bitcraze/crazyflie-lib-python">cflib</a>. Installation Instructions can be found on the repo README.

### Compilation ###

Checkout the <b>Flight-tests</b> branch. and complie using: 

```
Make clean
Make all PLATFORM=cf2b
```

To flash the cf using the radio:

``` 
Make cload
```

### Setting Parameters ###

Set the parameters for the firware using the <b>updateParameters.py</b> utility within the testScripts folder (has usefull python utils).
Once the crazyballon is on, run the following depending on your configuration:

For a non-camera configuration:
```
python3 updateParameters.py params_without_camera.json
```
For a camera configuration:
```
python3 updateParameters.py params_with_camera.json
```

### Testing Hover ###

For testing a takeoff &amp; hover use the following (also in testScripts)
```
python3 flightTimeTest.py
```
<i>flightTimeTest.py</i> may be used as a base for other flight tests as it has all the basic framework for starting off.

```
Note that the CF address is hardcoded within the python scripts and may require modification
```

# SLAM Integration #

The SLAM integration requires the installation of a camera on the airship along with a reciever connected to the PC.
The Software requires a ROS enviroment and a catkin workspace. To set these up, follow instruction <a href="http://wiki.ros.org/melodic/Installation">here</a> and <a href="http://wiki.ros.org/catkin/Tutorials/create_a_workspace">here</a>.

## Installation ##

### Cloning Required Repos ###
The following ros packages are required for the demo:
- usb_cam : used for streaming images from the reciever to a ROS topic. can be found <a href="https://github.com/ros-drivers/usb\_cam">here</a>.
- crazyflie_ros: used for communication with the crazyfile. can 

Please clone them into your catkin workspace (under src)


### Building workspace ###
Finish-off by building your catkin workspace using (from within the workspace top-level):
```
catkin_make
```
Overlay the workspace using:
```
source Devel/setup.sh
```
We are now ready to start up all the ROS nodes and ROS core.

## Usage ##

The demonstration script shows a Takeoff and calibration sequence (more info on the calibration can be found in the final project paper).

Start by building your catkin workspace using (from within the workspace top-level):
```
catkin_make
```
Overlay the workspace using:
```
source Devel/setup.sh
```
We are now ready to start up all the ROS nodes and ROS core.<br>












