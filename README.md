# Autonomous-differential-drive-robot
![](https://github.com/KaiXin-Chen/Autonomous-differential-drive-robot/blob/main/StopSign.png)
## Basic info
This is the course project for the Stanford cs237a (principle of robot autonomy) class. Contributors are Hao Li, Ran Li, Kaixin Chen and Zhengyang Wei. We employed the "ASL turtlebot" package built by the course instructors and implemented a variety of functions (in Python), ROS nodes, ROS topics, publishers and subscribers to achieve autonomous motion in some known environments. Note that because of the requirements of the Stanford honor code, the code cannot be made public, so please contact me at kaixinc@stanford.edu if you want to learn more about the project. Note that this document is entirely written by Kaixin Chen, so this document does not represent the perspectives of other groupmates in my group.
## Problem statement
According to the requirements of the class project, our robot is initialized in an unknown environment (unknown to the robot but known to the user) and should go through the following two stages to achieve autonomous motion. In both of the stages, the robot receives a goal position from either rViz(inputted by a person) or from another input of our choice. The robot's trajectory is planned by an A* algorithm avoiding all known obstacles while assuming all unknown parts of the environment are obstacle-free.
### Exploration stage.
First, we use Gazebo and rViz to simulate and manually manipulate the robot in an unknown environment. What is meant by manually manipulating here is that we have to manually set a series of goals on rViz for the robot such that the robot will see the entire environment and since the robot can only avoid obstacles those are already been seen these manually set goals should also help the robot to prevent from banging into obstacles those are unknown and unseen by the robot when the path was planned. The robot will use the lidar signal to construct a map as it explores. Also, there should be multiple objects in this environment. We chose to have animals (very important for the next stage), pedestrians, stop signs and speed limit signs in our environment. Our robot should also be able to identify these objects and record their location of these objects. We have decided that beyond the minimal requirements of the project we also mark the positions of each animal on rViz using markers and make our robot stop at a stop sign and slow down at a speed limit sign.
### Autonomous stage     
When the map is fully known, the positions of all obstacles are known, so the robot can then achieve full autonomous motion. The robot should be able to visit a series of arbitrary locations (in our case, it is which animal the user wants to visit) without hitting any obstacles. We should also design an interface so the robot can then visit that given animal autonomously. Like the exploration stage, we have decided that beyond the minimal requirements of the project we also make our robot stop at a stop sign and slow down at a speed limit sign.
## Approach Overview
### Architecture
The system architecture is shown below
![](https://github.com/KaiXin-Chen/Autonomous-differential-drive-robot/blob/main/Architecture.png)
<br>In the exploration stage the user manually controls the robot using rViz shown by the "Set Goal" arrow. Meanwhile, the detector (basically a convolutional neural network) is actively looking for animals, pedestrians and etc. In contrast in the autonomous stage, the user only needs to initiate "Rescuer" by running a python file shown by the "run Python arrow". This will initialize a publisher and help the user publish the animal that the user wants the robot to visit.
<br>Onece the desired destination is known to the robot, the Supervisor ROS node works with the navigator ROS node, where the navigator node is in charge of planning the path a closed-loop control of the robot and the state machine in the supervisor is in charge of handling multiple exception cases that the robot will encounter, for example, seeing a stop sign and seeing a speed limit.
### State Machine
Below shown more details about the state machine
![](https://github.com/KaiXin-Chen/Autonomous-differential-drive-robot/blob/main/State_machine.png)
## Result Overview
As the environment is fairly simple, we can achieve successful autonomous motion every time when a destination was set. Also, we received full marks for the project demo.
### Exploration stage
Our robot is capable of successfully constructing a map. Meanwhile, any user with some knowledge about the robot can manipulate the robot successfully with no collision in this stage.
![](https://github.com/KaiXin-Chen/Autonomous-differential-drive-robot/blob/main/exploration.png)
### Autonomous stage
It can achieve full autonomous motion without any user effort except by typing the desired destination in the terminal. (The green line in the rViz window is the automatically planned path. The blue, red, cyan and green points in rViz are the markers that make the position of different animals)
![](https://github.com/KaiXin-Chen/Autonomous-differential-drive-robot/blob/main/autonomous.png)
