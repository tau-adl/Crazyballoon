# Crazyballoon
Crazyflie modification to airship using balloon. Mainly Instructions on Installation &amp; Usage.

# Mechanics and Electronics #

Design files for both ECAD &amp; MCAD can be found on this <a href="https://github.com/tau-adl/crazybal-design-files"> repository </a>.
Assembly and more can be found in the <a href="https://github.com/tau-adl/Crazyballoon/blob/master/Final%20Project%20Documentation%20-%20Erez%20Gotlieb.pdf">final project paper</a> paper in this repo

# Crazyfile Firmware #

In order to fly the airship, a modified version of the firmware is needed.

## Instructions ##

The modified firmware, along with enviroment setup can be found on this <a href="https://github.com/tau-adl/crazyfile-firmware.git"> repository </a>.</br>
For some python utility scripts (and for cfclient) it is required to install <a href="https://github.com/bitcraze/crazyflie-lib-python">cflib</a>. Installation Instructions can be found on the repo README.

### Compilation & Flashing ###

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
The following ros packages are required in the <u>same workspace</u> for the demo:
- <b>usb_cam</b> : used for streaming images from the reciever to a ROS topic. Can be found <a href="https://github.com/ros-drivers/usb_cam">here</a>.
- <b>crazyflie_ros</b>: used for communication with the crazyfile. Can be found <a href="https://github.com/tau-adl/crazyflie_ros">here</a>.
- <b>orb_slam_2_ros</b>: implementation of the ORB SLAM 2 algorithm and linked to a ROS enviroments. Can be found  <a href="https://github.com/tau-adl/orb_slam_2_ros">here</a>.<br>
Please clone them into your catkin workspace (under <i>/src</i>)


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

The demonstration script shows a Takeoff and calibration sequence (more info on the calibration and TF can be found in the <a href="https://github.com/tau-adl/Crazyballoon/blob/master/Final%20Project%20Documentation%20-%20Erez%20Gotlieb.pdf">final project paper</a>).

In seperate shells start the following:

- Start by starting ROSCORE: ``` roscore ```
- Launch the usb_cam node: ```  roslaunch usb_cam usb_cam-test.launch ``` 
- Start the demo using: ``` roslaunch crazyflie_demo crazy_bal_demo.launch ```

The demo script will start the orb_slam_2 node once in the air using a launch file in the orb_slam_2_ros package.
The script automatically uses:
```
roslaunch orb_slam2_ros orb_slam2_crazybal_mono.launch
```
The launch file uses the config file (contains camera calibration that might need to be adjusted) found in<br> - <i> orb_slam2/config/crazybal_camera.yaml</i> in the ORB_SLAM_2 ROS package repo.










