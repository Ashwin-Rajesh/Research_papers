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
- Motivations
  - **cheap and easy to use** data collection device
  - Obtaining **diverse data** about hard to access scenarios
  - Data must be **easily transferred** to real robots
- The device was given to several volunteers who did day-to-day tasks using the device. 12 hours of gripper-centric RGB-D video was recorded, labelled with the signal from push button used to control the gripper.

### Data processing

- Trajectory of camera is extracted from video using standard computer vision algorithms (using SIFT, RANSAC, and SVD). It is refined using ICP
- Since gripper is placed in a fixed position relative to camera, the position and orientation of the gripper can be found be using a rigid body transform which would have been computed before-hand
- The videos are split into short clips of each attempt. The frames before button push (when gripper is open) is the pre-grasp trajectory and the frames till the gripper is opened again is the post-grasp trajectory.
- Pixel mask of target can also be obtained by detecting pixel regions that are stationary in the post-grasp trajectory video.

### Closed-loop vision-based Grasping system

- We use reinforcement learning, specifically Q learning for deciding the control strategy.
- Goal is to find optimum **policy** that selects actions based on current state of the system that optimizes a total expected reward.
- States are the image observations from the camera, and the actios are rigid transforms encoding relative rotation and translation from current pose to the next. Motion planning and control is done by proportional-derivative controllers with inverse kinematic solvers.
- Gripper is closed by monitoring the space between the grippers and using depth value to chack if an object is between the grippers.
- Pre-grasp trajectories start 50cm away from the scene and terminates 40 state transitions later.
- The next states (image) are estimated from current states using view-based rendering
- Human demonstration data is used to train the Q function.
- Q function is a measure of how good each action is. It takes current state and action as input. It ideally is the sum of discounted (exponentially weighted) rewards from all future actions (which would all be optimal)
- The algorithm works as follows :
  1. A 3D representation of the scene is created (from previous observations also)
  2. Various future states for different possibilities of actions that can be taken is rendered using the 3D reconstruction
  3. Q value is found by a neural network for each of these states, and the action with optimal Q value is selected

## What i did not understand

- Q learning
- How is reward decided?
- Markov decision process
- View based rendering
- SIFT, RANSAC, SVD for visual odometry
- ICP for refinement of trajectory

---

## Abbreviations
- DOF : Degrees of freedom
- RGB-D : Red Green Blue - Depth
- SIFT : Scale Invariant Feature Transform
- RANSAC : RANdom SAmple Consensus
- SVD : Singular value decomposition 
- ICP : Iterative closest point

---

## References
- Q learning : https://towardsdatascience.com/simple-reinforcement-learning-q-learning-fcddc4b6fe56
- Q learning : https://www.youtube.com/watch?v=qhRNvCVVJaA
