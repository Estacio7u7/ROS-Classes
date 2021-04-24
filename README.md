ROS_firstCourtClass
=============================

This is the 9th semester class, ROS, took in 2021-1. This are notes taken in class.

RBX1 Robot Example
============================

**First Part: Install RBX1 repository**

In a terminal, first go to your ROS_package source folder. Write:

'''
cd ~/ROS_package/src
'''

Then, copy the RBX1 repository from author's github:

'''
git clone https://github.com/pirobot/rbx1.git
'''

Or you can install directly from ROS repository:

'''
sudo apt-get install ros-kinetic-rbx1
'''
if you get any trouble, try installing ROS dependencies:
'''
sudo apt-get install python-rosinstall
'''
 

ejecutar el launch---$ roslaunch rbx1_bringup fake_turtlebot.launch; otra forma es directamente a la carpeta y ejecutar el launch (carga el modelo del robot con las caracteristicas de movimiento del turtlesim antes de ejecutar el nodo)
roscore
rosrun rviz rviz -d`rospack find rbx1_nav`/sim.rviz
rosrun turtlesim turtle_teleop_key
reviso los topics actuales rostopic list matando en teleop para saber cual es el topic del launch
reviso el suscriptor del topic que quiero filtrar y reviso el nombre del nodo
voy a launch y dentro del nodo correspondiente agrego la linea de remap para que los datos que me pide el topic se enlacen con el topic que deseo, en este caso el teleop (como esta actualmente a como ahora se llamará) 
<remap from="/cmd_vel" to="/turtle1/cmd_vel"/>

 

ahora sí como se modifico el launch debo matar el roslaunch ya ejecutado y volver a correrlo para que reciba los cambios, ya se comunica el terminal con el rviz 

 

si quiero modificar la velocidad que envía el teleop, mato el teleop y ejecuto $ rosparam set teleop_turtle/scale_linear 0.5
vuelvo a correrlo.
