# Planning and Control

[Return Home](/../../)

## Quadrotor Dynamic Simulation and Control

I developed this project in coordination with the Aerial Robotics section of the Robot Mobility course at Carnegie Mellon University taught by Nathan Michaels. He provided general skeleton code to facilitate a simulation in Matlab. Given this code, I implemented each component of the software architecture shown in the following image. I developed the system to create a trajectory from a series of waypoints, then execute the commanded trajectory. I implemented a nested loop control scheme with position control in the outer loop and attitude control in the inner loop. For the control methods, I compared the effectiveness of both PD and LQR controllers. Finally, I implemented a linear motor model and dynamics model for the system.


<p align="center">
  <img align="center" src="images/quadrotor/software_diagram.png" />
</p>


I evaluated the system and tuned control parameters by running the simulated drone through several trajectories. The trajectories included hover, step input, line-tracking, bounded z-acceleration, ellipse, and pirouette. You can see the extent of my testing and results in this [report](images/quadrotor/air_report.pdf).


## Autonomous Vehicle Club

I'm adding this project, not because it is particularly well done, but rather becuase it was my first experience in robotics. At Utah State University I participated in the Autonomous Vehicle Club. We had a 1/10 scale RC car retrofitted with an IMU and a lidar. We used this car to participate in the Sparkfun Autonomous Vehicle Competition. I joined the team during my Junior year at USU. In my first year on the team I implemented Google Cartographer to improve our SLAM capability. This is also when I became familiar with Linux and ROS. 

In my second year with the team I helped fix a variety of bugs with the low level velocity controller, helped recruit new team members, and improved the simulation capabilities of the team. In coordination with a Mobile Robotics course taught by Dr. Greg Droge, I created a URDF representation of the vehicle. I then took a simple go-to-goal controller provided by Dr. Droge and implemented a bicycle model vehicle to represent the car. You can see the result of that work in this [repository](https://github.com/eichmeierbr/avc_urdf). This video shows my first attempts into vehicular robotics.

<img align=center src="./images/avc/avc_g2g.gif" />

[Return Home](/../../)
