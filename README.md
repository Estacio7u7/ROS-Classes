ROS_Course
=============================

This is the 9th semester class, ROS, took in 2021-1. This are notes taken in class.

RBX1 Robot
============================

**First Part: Install RBX1 repository**

In a terminal, first go to your ROS_package source folder. Write:
```
cd ~/ROS_package/src
```
Then, copy the RBX1 repository from author's github:
```
git clone https://github.com/pirobot/rbx1.git
```
Or you can install directly from ROS repository:
```
sudo apt-get install ros-kinetic-rbx1
```
*In this case, we are using Kinecti-Kame distro, change that for yours and check compatibility before.*

if you get any trouble, try installing ROS dependencies:
```
sudo apt-get install python-rosinstall
```
 
**Second Part: Executing LAUNCH file**

A .launch file is made to execute many packages and nodes in one go. Here we can see how it works with the next line in a terminal:
```
roslaunch rbx1_bringup fake_turtlebot.launch
```
*Another way is going directly to the .launch containig folder and executing it directly there*

**Third Part: Making changes to the .launch file**

First, we need to know what are we doing. For this example, we need to change a *topic* inside the launch file (We will define *topic* later) to make this robot compatible with the teleop_key characteristic from turtlebot example included in ROS.Lets check wich is that *topic*.
1. In a terminal, start ROS:
```
roscore
```
2. In a new terminal, run a rviz app (this will load the model inside a 3D environment):
```
rosrun rviz rviz -d`rospack find rbx1_nav`/sim.rviz
```
3. In a new terminal, run the teleoperator key characteristic:
```
rosrun turtlesim turtle_teleop_key
```
4. Current running topics:
To know what are we going to change, let's look the current topics in a new terminal:
```
rostopic list
```
cheking the current topics, we can see that there are two topics that looks very similar: */cmd_vel* and */turtle1/cmd_vel*.
If we kill the teleop_key process, the topic called */turtle1/cmd_vel* will disappear and that is the singal we were looking for.

5. remaping topics inside a .launch file:
Going to the .launch containing folder, we can open and edit this in any text editor like gedit in the graphic interface. We're looking for the part of the code that runs the node called *arbotix* marked with "< -- >" symbols, in a new line inside this segment of code we will write:
```
<remap from="/cmd_vel" to="/turtle1/cmd_vel"/>
```
Let's save, kill the process and repeat the steps 2 and 3. Now we can control the arbotix rbx1 robot inside the rviz environment with the teleop_key characteristic from the ROS turtle bot example.To be sure, I let you the modified launch file uploaded here.

**Fourth part: changing parameters inside a command line**

Let's change the speed of the rbx1 movement directly from command line. This is not permanent, and everytime the next time we start the example the speed will be by default.

The command line is as follows:
```
$ rosparam set teleop_turtle/scale_linear 0.5 && rosrun turtlesim turtle_teleop_key
```
