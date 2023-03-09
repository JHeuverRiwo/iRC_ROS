# iRC ROS Examples

This package showcases how to implement Igus Robot Control ROS2 for different usecases.

**Note: Starting the examples directly over the launch files in this package is not recommended as of now. The launch file does not wait for the moveit+ros2_control stack to be finished initialising, which causes jerky motions at startup**

## Pick&Place (MoveIt)
![](doc/pick_and_place.gif)

This simple example showcases point-to-point, linear and axis movements, as well as how to interact with the gripper via its controller's service.

For further MoveIt commands see [here](https://moveit.picknik.ai/humble/doc/examples/examples.html#using-moveit-directly-through-the-c-api).

### Usage

``` bash
# Start moveit with the right gripper parameter
$ LC_NUMERIC=en_US.UTF-8 ros2 launch irc_ros_moveit_config demo.launch.py gripper:="ext_dio_gripper"

# Once the startup is complete run
$ ros2 run irc_ros_examples pick_and_place
```

## Pick&Place-Vacuum (MoveIt)
![](doc/pick_and_place_vacuum.gif)

Uses the Schmalz ECBPMI vacuum gripper for a vertical pick and place application. This showcases using the ECBPMI Controller, specifically how to use the service calls. It is also planned to use different coordinate systems for the different trays in the future.

### Usage

``` bash
# Start moveit with the right gripper parameter
$ LC_NUMERIC=en_US.UTF-8 ros2 launch irc_ros_moveit_config demo.launch.py gripper:="schmalz_ecbpmi"

# Once the startup is complete run:
$ ros2 run irc_ros_examples pick_and_place_vacuum
# This will run the process in an infinite loop
```

## Basic Navigation (Nav2 Simple Commander)
**WORK IN PROGRESS EXAMPLE**
This example should showcase simple movements with the mobile platform over the [Nav2 Python API](https://navigation.ros.org/commander_api/index.html). It is also useful for testing Nav2 parameters.

The platform should drive over the four corners of a square and end where it started. While it achieves that goal already, it is rather slow due to unnecessary turning and detours.

## BaristaBot (MoveIt + Nav2 + more)
**Only a collection of ideas for now**
 - Coffee delivery showcase application
 - IoT Coffeemachine, [official way](https://api-docs.home-connect.com/quickstart) or [reverse engineered way](https://github.com/osresearch/hcpy)
   - Second way is available offline, but maybe not a good thing to use something reverse engineered if we publish this?
 - Gripper(s)
   - "Dumb", form-fitting gripper for a specific cup,
   - Normal two-finger gripper
 - Coffee Cup localisation (marker or image recognition ?)
   - Camera (Webcam, Depth imaging like Oak-D, ...)
 - Test and film the process
 - Nav2 Behaviour Trees
 - Web interface for ordering

### Process
Turn the following process into a Nav2 compatible BT
 - Battery low?
 - Is coffee machine (cm) ready?
   - Notify assistant to refill, empty machine
 - Coffee ordered? (Via web ui?)
 - Grab empty cup
   - No empty cups left? Notify assistant
 - Bring empty cup in position
 - Start selected CM program
 - Wait for CM
 - Grab cup again
 - Drive slowly to counter
 - Place cup there
 - Drive back to waiting position

#### Questions
 - Can the CM fail during the process?
 - Different cups for different drinks possible?
 - Predefined cup position or detection?
 - Feedback for gripping success/failure
 - Positions hardcoded, markers, image detection, ... ?
 - Keep out zones?

### Links
 - https://navigation.ros.org/plugin_tutorials/docs/writing_new_bt_plugin.html
 - https://navigation.ros.org/tutorials/docs/using_groot.html

## TODO
 - Make exiting the files not require a KILL signal to quit
 - Use multiple TFs for vacuum example
 - Fix launch files causing jerky movement on startup
 - Improve nav2_simple_commander_example and add a video
 - Implement BaristaBot