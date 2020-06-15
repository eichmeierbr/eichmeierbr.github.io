# Machine Learning Projects

## Reinforcement Learning for a Robotic Arm

For the Robot Autonomy course at Carnegie Mellon, I worked on teaching a robotic arm to place groceries in a cupboard using reinforcement learning. The project was originally intended to be realized on a physical arm, but restrictions to the COVID-19 pandemic caused us to move to a simulated environment. We used RLBench and V-Rep to simulate the arm. You can find the code for this project in my git repository [here](https://github.com/eichmeierbr/robo_autonomy_project).

<img align=center src="images/grocery_rl/grocery_soup.gif" />

This project focused on solving one of the major problems of facilitating machine learning in the real world: resetting the environment. When training in simulation, a "reset" call is made at the end of a training episode to return the environment to the original state. In the real world, there is no such "reset" call. In reality, the "reset" function is done by a research assistant who manual restores the original environment state. This method is slow and expensive. In a team of 3, I explored the possibility of programming a robot to reset the environment itself to facilitate full-time unsupervised training. This video shows the resetting portion of the task for performing the forward task manually.

<img align=center src="images/grocery_rl/grocery_resetting.gif" />

My teammates worked on the resetting task, which involved removing objects from the cupboard and standing up objects that were knocked down. I worked on the learning task which involved using reinforcement learning to grasp, and place the objects in the cupboard. I used the [TensorForce](https://tensorforce.readthedocs.io/en/latest/) library to implement a Deep Q-Network. I separated the grasp task and the place task to learn the respective behaviors independently. For each task, I reduced the state space and action space as much as possible to speed up convergence due to the tight schedule of the project. I also did bounds checking on the action space to protect the robot within the environment and prohibit impossible joint configurations.

<p float="center">
  <img src="images/grocery_rl/grocery_mustard.gif" width="400" />
  <img src="images/grocery_rl/grocery_tuna.gif" width="400" />
</p>


The report and presentation my teammates and I made for this project can by found here:

[Report](images/grocery_rl/Autonomy_Report.pdf)

[Presentation](https://docs.google.com/presentation/d/1j3ABuQvJndEL6WjDsbPbcUgUFTWPosp4RI9eBwghe20/edit?usp=sharing)


