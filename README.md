# r2d2-urdf-ros2
R2D2-inspired multi-joint robot built with URDF and animated in RViz2 using robot_state_publisher — ROS2 Jazzy

# R2D2 URDF Tutorial — ROS2

A ROS2 C++ package that builds an R2D2-inspired multi-joint robot using URDF,
visualizes it in RViz2, and animates it moving in a circle using `robot_state_publisher`.

---

## 📸 Demo

![R2D2 robot moving in RViz](https://youtu.be/TTFNajsD9FA?si=HTDlEewnB1rD_RFY)

---

## 🤖 What This Does

- Defines a multi-joint R2D2-like robot in URDF (`.urdf.xml`)
- A C++ node continuously publishes `JointState` messages, animating the joints
- `robot_state_publisher` computes forward kinematics and broadcasts TF transforms
- RViz2 reads the TF tree and renders the robot moving in a circular path

### Motion Pipeline
```
cpp_node → /joint_states → robot_state_publisher → /tf → RViz2
```

---

## 📁 Package Structure
```
urdf_tutorial_cpp/
├── CMakeLists.txt
├── package.xml
├── launch/
│   └── launch.py           # Launches robot_state_publisher + RViz2 + the cpp node
├── src/
│   └── urdf_tutorial.cpp   # Publishes joint states to animate the robot
└── urdf/
    ├── r2d2.urdf.xml       # Full robot URDF definition
    └── r2d2.rviz           # RViz2 configuration file
```

---

## ⚙️ Prerequisites

- ROS2 (tested on **Jazzy**)
- `robot_state_publisher`
- `joint_state_publisher`
- RViz2

Install dependencies:
```bash
sudo apt install ros-jazzy-robot-state-publisher \
                 ros-jazzy-joint-state-publisher \
                 ros-jazzy-rviz2
```

---

## 🚀 Build & Run
```bash
# Clone into your ROS2 workspace
cd ~/ros2_ws/src
git clone https://github.com/codeubermensch/r2d2-urdf-ros2

# Build
cd ~/ros2_ws
colcon build --packages-select r2d2-urdf-ros2
source install/setup.bash

# Launch
ros2 launch urdf_tutorial_cpp launch.py
```

RViz2 will open automatically and you will see the R2D2-like robot animating with all joints moving.

---

## 🧠 How It Works

| Component | Role |
|---|---|
| `r2d2.urdf.xml` | Defines all links, joints, geometry, and colors of the robot |
| `urdf_tutorial.cpp` | C++ node that publishes changing joint angles over time |
| `robot_state_publisher` | Subscribes to `/joint_states`, computes FK, publishes `/tf` |
| RViz2 | Reads `/tf` and renders each link at its correct 3D pose |

The C++ node uses **sine and cosine functions** over time to smoothly vary each
joint angle, producing circular and oscillating motion — no physics engine involved.
This is pure kinematic visualization.

---

## 📚 Reference

Built by following the official [ROS2 URDF Tutorial](https://docs.ros.org/en/jazzy/Tutorials/Intermediate/URDF/URDF-Main.html).

---
