# Grasping in the Wild: Learning 6DoF Closed-LoopGrasping from Low-Cost Demonstrations

Authors : Shuran song, Andy Zheng, Johnny Lee, Thomas Funkouser
Original paper : https://arxiv.org/pdf/1912.04344.pdf

---

## What i understood

### Abstract
- High degrees of freedom and ability to dynamically react to the environment is important for grasping using robotic manipulators.
- Most grasping algorithms use open-loop systems and top-down movement (4DOF - x, y, z, yaw), due to lack of training data (or either one)
- A low-cost device is developed to collect data on diverse day-to-day grasping tasks from human volunteers.
- Reinforcement learning is used, along with this data to train a 6-Degree of freedom closed loop grasping model.

### Grasping data aquisition
- One major obstacle to achieving both 6DOF and closed-loop control is lack of training data. Self-supervised trial and error is not effective because as DOF increases and data becomes more diverse (static objects v/s dynamic, moving objects), the time and effort required to get an optimum solution by trial and error increases exponentially.
- Data is collected using a handheld gripper with an RGB-D camera setup to be similar to that of the real robot. The gripper uses a plastic grabber with a binary open/close function, controlled by the user using a push button. designed to be similar to the RG2 gripper used in the actual setup 
- Previous approaches
  - Purely self-supervised learning : Robot is exposed only to limited environments.
  - Human annotations and human teleoperation data : Require trained operators and data is limited to certain environments.
  - Using data of grasping using human hands : Big gap between kinematics of human hands and robotic grippers make transfer of knowledge hard
- This approach uses a **cheap and easy to use** data collection device, giving **diverse data** which can be **easily transferred** to real robots
- 

---

## Abbreviations
- DOF : Degrees of freedom
- RGB-D : Red Green Blue - Depth
