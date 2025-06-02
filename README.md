## Robot Package Template

This is a GitHub template. You can make your own copy by clicking the green "Use this template" button.

It is recommended that you keep the repo/package name the same, but if you do change it, ensure you do a "Find all" using your IDE (or the built-in GitHub IDE by hitting the `.` key) and rename all instances of `my_bot` to whatever your project's name is.

Note that each directory currently has at least one file in it to ensure that git tracks the files (and, consequently, that a fresh clone has direcctories present for CMake to find). These example files can be removed if required (and the directories can be removed if `CMakeLists.txt` is adjusted accordingly).

## Neccesary Packages for Jazzy Jalisco:
- sudo apt install ros-jazzy-xacro (To be able to merge multiple files for forming URDF for robot)
- sudo apt install ros-jazzy-gz-ros-pkgs (For Gazebo simulation)
- sudo apt install ros-jazzy-twist-mux (To be able to subscribe to messages that enable to controller to function for teleop)
- If using compressed images and want to visualize: rqt_image_view package

### For ROS2 Control:
- sudo apt install ros-jazzy-ros2-control
- sudo apt install ros-jazzy-ros2-controllers
- sudo apt install ros-jazzy-gz-ros2-control

## ROS2 Jazzy Development Setup with Gazebo Simulation

To build the package:

colcon build --symlink-install --packages-select my_bot

To launch:

ros2 launch my_bot rsp.launch.py

For RVIZ Visualization:

Open rviz.

- rviz2

In rviz, add TF and RobotModel in the window on the right.

![rviz_image](images/rviz_1.png)

To view the wheels since they are continous/ rotating, run the joint_state_publisher_gui.

ros2 run joint_state_publisher_gui joint_state_publisher_gui 

XACROS:
- robot.urdf: brings all xacro/ urdf's together as one.
- robot_core: defines the components of the robot and the component's coordinate frames.

Notes:
- Joints come first, and are the coordiante frames.
- Links come next, and are the associated material in the model.


## Launching Gazebo Simulation (Gazebo Harmonic):
  If you have no gazebo installed: 
- sudo apt-get install ros-jazzy-gz-ros-pkgs

- ros2 launch my_bot rsp.launch.py use_sim_time:=true
In another terminal:
- ros2 launch gazebo_ros gazebo.launch (for humble)
- **ros2 launch ros_gz_sim gz_sim.launch.py (for jazzy)**
  - Launching a specific world, add: world:="./src/practice_robot/worlds/perc_tank.world"

Spawning:
- ros2 run gazebo_ros spawn_entity.py (Humble)
- ros2 run ros_gz_sim create -topic robot_description // Gives the robot description to Gazebo.
Notes:
- gz sim (opens main window for gazebo with example projects)
- gz sim shapes.sdf -v4 (example simulation)
- gz topic -l (list topics running in gazebo)

### Launch Gazebo simulation all at once:
- ros2 launch my_bot launch_sim.launch.py world:="./src/practice_robot/worlds/perc_tank.world"

*I recommend running from an external terminal to VSCode. I like Tilix as my terminal platform.*

### For Gazebo/ robot Teleop:

With Computer keyboard:
- ros2 run teleop_twist_keyboard teleop_twist_keyboard

With Logitech/Game Controller:
- teleop_twist_joy -- teleop_node
- joy -- joy_node


### Useful commands:

- ros2 pkg list | grep nameOfThing
