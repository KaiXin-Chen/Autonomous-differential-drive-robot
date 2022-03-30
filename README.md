# Autonomous-differential-drive-robot
## Basic info
This is the course project for Stanford cs237a (principle of robot autonomy) class. Contributors are Hao Li, Ran Li, Kaixin Chen and Zhengyang Wei. We employed the "ASL turtlebot" package built by the course instructors and implemented a variety of functions (in Python), ROS nodes, ROS topics, publishers and subscribers to achieve autonomous motion in some certain enviroment. Note that because of the requirments of the Stanford honor code, the code cannot be made public, so please contact me at kaixinc@stanford.edu if you want to learn more about the project. Note that this document is entire written by Kaixin Chen, so this document do not represent the perspectives of other groupmates in my group.
## Problem statement
According to the requirement of the class project, our robot is initialized in an unkown enviroment and should go through the following two stages to achieve autonomous motion. In both of the stage, the robot recieve a goal position from either rViz(inputted by a person) or from another input of our choice. The robot's trajactory is planned by an A* algorithm avioding all konwn obstacles while assume all unkown part of the enviroment is obstacle free.
### Exploration stage.
First we use gazebo and rViz to simulate and manually manipulate the robot in a unkown enviroment. What is meant by manully manipulate here is that we have to manually set a series of goals on rViz for the robot such that the robot have seen the entire enviroment and since the robot can only avoid obstacle those are already been seen these manually set goals should also help the robot ro prevent from banging into obstacles those are unknown and unseen by the robot when the path was planned.  The robot will use the ladar signal to construct a map as it explores. Also, there should be multiple objects in this enviroment. We chose to have animals (very important for the next stage), pedestrian, stop sign and speed limit sign in our enviroment. Our robot should also be able to identify these objects and record the location of these objects. We have decided that beyongd the minimal requirments of the project we also mark the positions of each animal on rviz using markers and make our robot stop at a stop sign and slow down at a speed limit sign.
### Autonomous stage
After the map is fully known, the position of all obstacles are known, so the robot can then achieve full autonomous motion. The robot should be able to visit a series of arbitrary locations without hitting any obstacles. We should also design an interface so the robot can then visit that given animal autonomously. Like the exploration stage, we have decided that beyongd the minimal requirments of the project we also make our robot stop at a stop sign and slow down at a speed limit sign.
## Approach Overview
### Architecture
The system architecture is shown below
![](https://github.com/KaiXin-Chen/Autonomous-differential-drive-robot/blob/main/Architecture.png)
<br>In the exploration stage the user manually control the robot using rViz shown by the "Set Goal" arrow. Meanwhile, the detector (basically a convolutional neural network) is activly looking for animals, pedestrians and etc. In contrast in the autonomous stage, the user only need to initiate "Rescuer" by running a python file shown by the "run Python arrow". This will initialize a publisher and help the user publish the animal that the user want the robot to visit.
<br>Onece the desired destination is known to the robot, the Supervisor ROS node works with the navigator ROS node, where the navigator node is in charge of planning the path a closed loop control of the robot and the state machine in the supervisor is incharge of handling multiple exception cases that the robot will encounter, for example, seeing a stop sign and seeing a speed limit.
### State Machine
Below showns more details about the state machine
![](https://github.com/KaiXin-Chen/Autonomous-differential-drive-robot/blob/main/State_machine.png)
## Result Overview
As the enviroment is fairly simple, we can achieve successful autonomous motion everytime when a destenation was set. Also we recieved full marks for the project demo.
### Exploration stage
Our robot is capable of successfully contructing the map and record the 
