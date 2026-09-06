# RoboticArm

A 4-DOF robotic arm designed for robotic manipulation and kinematic control, using **5840 31ZY D8 geared DC motors** and **ACS5600 magnetic encoders** for joint position feedback.

The project focuses on developing a compact robotic manipulator with closed-loop joint control, allowing the arm to estimate its configuration and perform forward and inverse kinematics.

## Overview

The robotic arm has four degrees of freedom (DOF), providing control over the position and orientation of the end effector.

<p align="center">
  <img src="https://github.com/user-attachments/assets/21e0ab85-6a76-4470-b7a2-4222a7c9ee6b" width="373">
</p>

### Degrees of Freedom

| DOF | Joint                 | Function                                      |
| --: | --------------------- | --------------------------------------------- |
|   1 | Shoulder              | Controls the main elevation of the arm        |
|   2 | Elbow                 | Controls the extension and folding of the arm |
|   3 | Wrist                 | Adjusts the orientation of the wrist          |
|   4 | End Effector Rotation | Rotates the end effector around its axis      |

## Mechanical System

The arm uses **5840 31ZY D8 geared DC motors** to drive the joints. The geared motors provide the torque required to move the arm while maintaining a relatively compact mechanical design.

Each controlled joint is equipped with an **ACS5600 magnetic encoder**, providing angular position feedback.

The encoder feedback can be used to determine the actual joint position rather than relying exclusively on motor commands.

### Main Components

* 4× 5840 31ZY D8 geared DC motors
* 4× ACS5600 magnetic encoders
* Mechanical joints and linkages
* Motor drivers
* Arduino Mega 2560
* 2x 12v 7A Batteries w/BMS
* 2x MG996r 

## Control Architecture

The robotic arm is intended to operate using closed-loop position control.

The general control loop is:

```text
Target Joint Position
        ↓
   Controller
        ↓
    Motor Driver
        ↓
      Motor
        ↓
      Joint
        ↓
    Encoder
        ↓
  Joint Position
        ↓
     Feedback
        └──────────────→ Controller
```

The magnetic encoders provide the feedback required to calculate the current angular position of each joint.

This allows the controller to compensate for effects such as mechanical load, friction, gearbox backlash and external disturbances.

## Kinematics

The arm's configuration is represented by its four joint variables:

```text
q = [q₁, q₂, q₃, q₄]
```

where:

* `q₁` → Shoulder angle
* `q₂` → Elbow angle
* `q₃` → Wrist angle
* `q₄` → End effector rotation

The project will use the joint measurements to calculate the robot's configuration and perform kinematic calculations.

### Forward Kinematics

Forward kinematics determines the position and orientation of the end effector from the joint angles.

```text
Joint Angles
     ↓
Forward Kinematics
     ↓
End Effector Pose
```

The transformation between links can be represented using homogeneous transformation matrices:

```text
T₀⁴ = T₀¹ · T₁² · T₂³ · T₃⁴
```

The final transformation matrix describes the position and orientation of the end effector relative to the robot base.

### Inverse Kinematics

Inverse kinematics determines the required joint angles for a desired end-effector position and orientation.

```text
Desired End Effector Pose
          ↓
   Inverse Kinematics
          ↓
    Joint Positions
          ↓
    Motor Controllers
```

This will allow the arm to receive Cartesian coordinates and convert them into individual joint commands.

## Encoder Feedback

The **ACS5600 magnetic encoders** are used to measure the angular position of the joints.

The measured position can be represented as:

```text
θ₁, θ₂, θ₃, θ₄
```

These measurements are used to estimate the current robot configuration and close the control loop.

Future versions may implement individual PID controllers for each joint:

```text
Position Error
      ↓
     PID
      ↓
 Motor Command
      ↓
    Joint
      ↓
   Encoder
      └──────→ Feedback
```

## Project Goals

* Develop a functional 4-DOF robotic arm
* Implement reliable joint position feedback
* Implement forward kinematics
* Implement inverse kinematics
* Develop closed-loop joint control
* Characterize motor and gearbox performance
* Improve positioning accuracy
* Develop a modular control architecture
* Integrate the arm with higher-level robotic systems

## Future Improvements

Possible future developments include:

* Individual PID control for every joint
* Joint torque estimation
* Trajectory planning
* Cartesian-space control
* Motion interpolation
* Workspace visualization
* ROS/ROS 2 integration
* Computer vision for object detection
* Automatic pick-and-place
* Collision detection
* Improved mechanical transmission
* Higher-resolution joint sensing

## Project Status

**Development**

The mechanical and electronic architecture is being developed, with the control and kinematics systems planned around encoder-based joint feedback.

## License

This project is open-source. See the repository license for more information.
