# Autonomous-differential-drive-robot
## Basic info
This is the course project for Stanford cs237a (principle of robot autonomy) class. Contributors are Hao Li, Ran Li, Kaixin Chen and Zhengyang Wei. We employed the "ASL turtlebot" package built by the course instructors and implemented a variety of function to achieve autonomous motion in some enviroment. Note that because of the requirments of the Stanford honor code, the code cannot be made public, so please contact me if you want to learn more about the project. Note that this document is entire written by Kaixin Chen, so this document do not represent the perspectives of other groupmates in my group.
## Problem statement
According to the requirement of the class project, our robot is initialized in an unkown enviroment and should go through the following two stages to achieve autonomous motion.
### Exploration stage.
First we use gazebo and rViz to simulate and manually manipulate the robot in a unkown enviroment. As the map is unkown, the person manupulating should help robot avoid unseen obstacles at this stage. The robot will use the ladar signal to construct a map as it explores. Also, there are multiple objects in this enviroment. We chose to have animals (very important for the next stage), pedestrian, stop sign and speed limit sign in our enviroment. The robot should also record the location of these objects.
### Autonomous stage
After the map is fully known, the robot can now achieve full autonomous motion. We should design an interface so the robot can then visit that given animal autonomously.

## Approach Overview

We initialize a new publisher in ROS and this new publisher will help the user to publish the destination information, namely which animal the user wants to visit.

## Result Overview
As the enviroment is fairly simple, we can achieve successful autonomous motion everytime when a destenation was set. Also we recieved full marks for the project demo.
### Exploration stage
Our robot is capable of successfully contructing the map and record the 
