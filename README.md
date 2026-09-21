# 🤖 ROS 2 Robotics Workshop

## From ROS 2 Fundamentals to TurtleBot3, Gazebo & SLAM

> **A complete hands-on 2-day ROS 2 workshop for engineering students**
>
> Learn ROS 2 by building, inspecting, controlling and debugging robotic systems — starting with `turtlesim` and progressing to TurtleBot3 simulation, LiDAR, TF and SLAM.

---

<p align="center">

![ROS 2](https://img.shields.io/badge/ROS%202-Humble-blue?style=for-the-badge)
![Ubuntu](https://img.shields.io/badge/Ubuntu-22.04-orange?style=for-the-badge)
![Python](https://img.shields.io/badge/Python-3.x-yellow?style=for-the-badge)
![Gazebo](https://img.shields.io/badge/Gazebo-Simulation-lightgrey?style=for-the-badge)
![License](https://img.shields.io/badge/Workshop-Educational-green?style=for-the-badge)

</p>

---

# 📚 Table of Contents

* [About This Workshop](#-about-this-workshop)
* [Learning Philosophy](#-learning-philosophy)
* [What You Will Learn](#-what-you-will-learn)
* [Prerequisites](#-prerequisites)
* [System Requirements](#-system-requirements)
* [ROS 2 Architecture](#-ros-2-architecture)
* [Workshop Roadmap](#-workshop-roadmap)
* [Day 1](#-day-1--ros-2-fundamentals)

  * [ROS 2 Introduction](#1-ros-2-introduction)
  * [Environment Setup](#2-ros-2-environment)
  * [First ROS 2 Node](#3-your-first-ros-2-node)
  * [Nodes](#4-understanding-nodes)
  * [Topics](#5-topics)
  * [Publishing](#6-publishing-to-a-topic)
  * [Services](#7-services)
  * [Parameters](#8-parameters)
  * [Actions](#9-actions)
  * [Workspace](#10-workspaces-packages-and-colcon)
  * [Debugging](#11-ros-2-debugging)
  * [Day 1 Challenge](#12-day-1-challenge)
* [Day 2](#-day-2--ros-2-programming-turtlebot3-and-slam)

  * [Python ROS 2 Node](#13-create-your-first-python-ros-2-node)
  * [Publisher and Subscriber](#14-publisher--subscriber)
  * [Robot Control](#15-basic-robot-control)
  * [TurtleBot3](#16-turtlebot3)
  * [Gazebo](#17-gazebo-simulation)
  * [RViz2](#18-rviz2)
  * [TF](#19-tf--coordinate-frames)
  * [LiDAR](#20-lidar-and-laserscan)
  * [SLAM](#21-slam)
  * [Map Saving](#22-save-the-map)
  * [Navigation2](#23-introduction-to-nav2)
  * [Final Challenge](#24-final-project)
* [ROS 2 Command Cheat Sheet](#-ros-2-command-cheat-sheet)
* [Troubleshooting](#-troubleshooting)
* [Concept Summary](#-concept-summary)
* [Next Steps](#-what-to-learn-next)
* [Official Resources](#-official-resources)

---

# 🎯 About This Workshop

This workshop is designed to teach the **fundamentals of ROS 2 through practical implementation**.

Instead of learning ROS 2 only through theory, we follow a progressive robotics workflow:

```text
ROS 2 Fundamentals
        ↓
turtlesim
        ↓
Nodes
        ↓
Topics
        ↓
Services
        ↓
Parameters
        ↓
Actions
        ↓
Packages
        ↓
colcon
        ↓
Python ROS 2 Node
        ↓
TurtleBot3
        ↓
Gazebo
        ↓
LiDAR
        ↓
TF
        ↓
SLAM
        ↓
Mapping
        ↓
Navigation2
```

The objective is not simply to memorize commands.

The objective is to understand:

> **How software components communicate inside a robot.**

---

# 🧠 Learning Philosophy

Every concept follows this pattern:

```text
Understand
    ↓
Observe
    ↓
Run
    ↓
Inspect
    ↓
Modify
    ↓
Build
    ↓
Debug
```

For example, instead of simply saying:

> A ROS 2 topic is a communication mechanism.

We actually run:

```bash
ros2 topic list
```

Then:

```bash
ros2 topic echo /turtle1/pose
```

Then move the turtle.

Then inspect:

```bash
ros2 topic info /turtle1/pose
```

Then discover:

```bash
ros2 topic type /turtle1/pose
```

This allows students to **discover how ROS 2 works** rather than memorize definitions.

---

# 🎓 What You Will Learn

By the end of this workshop you will understand:

### ROS 2 Fundamentals

* ROS 2 architecture
* Nodes
* Topics
* Publishers
* Subscribers
* Messages
* Services
* Actions
* Parameters
* Packages
* Workspaces
* `colcon`

### ROS 2 Programming

* Python ROS 2 nodes
* Publishers
* Subscribers
* Callbacks
* `rclpy`
* ROS 2 message types

### Robotics

* `/cmd_vel`
* Odometry
* LiDAR
* `LaserScan`
* TF
* Coordinate frames
* RViz2
* Gazebo

### Autonomous Robotics

* SLAM
* Occupancy grids
* Mapping
* Localization concepts
* Navigation2 concepts

---

# 🛠 Prerequisites

You don't need advanced robotics knowledge.

Recommended:

* Basic Python
* Basic Linux terminal knowledge
* Basic programming concepts
* Basic understanding of robotics

You should understand:

```python
variables
functions
if / else
loops
classes
```

---

# 💻 System Requirements

Recommended workshop environment:

| Component | Recommended               |
| --------- | ------------------------- |
| OS        | Ubuntu 22.04              |
| ROS 2     | Humble                    |
| Python    | Python 3                  |
| RAM       | 8 GB minimum              |
| RAM       | 16 GB recommended         |
| CPU       | 4+ cores recommended      |
| Storage   | 30+ GB free               |
| GPU       | Recommended for Gazebo    |
| Internet  | Required for installation |

> **Important:** Gazebo simulation can be computationally heavy. Close unnecessary applications during the TurtleBot3 practical.

---

# 🧩 ROS 2 Architecture

The most important concept of the entire workshop:

```text
                     ROS 2

        ┌──────────────┐
        │ Camera Node  │
        └──────┬───────┘
               │
             Topic
               │
               ▼
        ┌──────────────┐
        │ AI Node      │
        └──────┬───────┘
               │
             Topic
               │
               ▼
        ┌──────────────┐
        │ Navigation   │
        │ Node         │
        └──────┬───────┘
               │
             Topic
               │
               ▼
        ┌──────────────┐
        │ Motor Node   │
        └──────────────┘
```

ROS 2 provides middleware and tools for communication between robotics software components. ROS 2's communication layer is designed around standards including DDS and IDL.

---

# 🗺 Workshop Roadmap

## DAY 1

```text
09:00  ROS 2 Introduction
09:30  Environment + CLI
10:00  turtlesim
10:30  Nodes
11:00  Topics
12:00  Topic Publishing
13:00  Lunch
14:00  Services
14:45  Parameters
15:15  Actions
15:45  Packages + Workspace
16:15  colcon
16:30  Debugging
17:00  Practical Challenge
17:30  Day 1 Review
```

## DAY 2

```text
09:00  ROS 2 Python
10:00  Publisher + Subscriber
11:00  Robot Control
11:30  TurtleBot3
12:00  Gazebo
13:00  Lunch
14:00  RViz2
14:30  TF
15:00  LiDAR
15:30  SLAM
16:15  Map Saving
16:30  Navigation2
17:00  Final Challenge
17:30  Final Review
```

---

# 🟦 DAY 1 — ROS 2 FUNDAMENTALS

---

# 1. ROS 2 Introduction

## What is ROS 2?

ROS 2 is a framework used to build robotic applications.

It provides:

* Communication
* Hardware abstraction
* Robot software libraries
* Tools
* Visualization
* Simulation support
* Navigation
* Perception
* Package management

Think of ROS 2 as the **communication and software infrastructure connecting different parts of a robot**.

---

# 2. ROS 2 Environment

## Check Ubuntu

```bash
lsb_release -a
```

You should see:

```text
Ubuntu 22.04
```

---

## Source ROS 2

```bash
source /opt/ros/humble/setup.bash
```

Check:

```bash
ros2 --help
```

### What does `source` do?

It loads ROS 2 environment variables and paths into the current terminal.

To make it permanent:

```bash
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
```

Then:

```bash
source ~/.bashrc
```

---

# 2.1 Install Basic Development Tools

```bash
sudo apt update
```

```bash
sudo apt install -y \
python3-colcon-common-extensions \
git
```

---

# 2.2 Install turtlesim

```bash
sudo apt install -y ros-humble-turtlesim
```

Run:

```bash
ros2 run turtlesim turtlesim_node
```

You should see the turtle window.

Stop it:

```text
Ctrl + C
```

---

# 3. Your First ROS 2 Node

Run:

```bash
ros2 run turtlesim turtlesim_node
```

Open another terminal:

```bash
source /opt/ros/humble/setup.bash
```

Run:

```bash
ros2 run turtlesim turtle_teleop_key
```

Use the arrow keys to control the turtle.

---

# 4. Understanding Nodes

A **node** is a running ROS 2 process responsible for a specific task.

Examples:

```text
Camera Node
LiDAR Node
Motor Node
Navigation Node
SLAM Node
```

---

## List Nodes

```bash
ros2 node list
```

Expected:

```text
/turtlesim
/teleop_turtle
```

---

## Inspect a Node

```bash
ros2 node info /turtlesim
```

Then:

```bash
ros2 node info /teleop_turtle
```

Look for:

```text
Publishers
Subscribers
Services
Actions
```

### Important idea

```text
Node = program doing a job
```

---

# 5. Topics

A topic is a named communication channel.

Example:

```text
teleop
   │
   │ publishes
   ▼
/turtle1/cmd_vel
   │
   │ subscribes
   ▼
turtlesim
```

---

# 5.1 List Topics

```bash
ros2 topic list
```

Important examples:

```text
/turtle1/cmd_vel
/turtle1/pose
/turtle1/color_sensor
```

---

# 5.2 Inspect a Topic

```bash
ros2 topic info /turtle1/cmd_vel
```

---

# 5.3 Find Message Type

```bash
ros2 topic type /turtle1/cmd_vel
```

Expected:

```text
geometry_msgs/msg/Twist
```

---

# 5.4 Inspect Message Definition

```bash
ros2 interface show geometry_msgs/msg/Twist
```

You will see:

```text
Vector3 linear
Vector3 angular
```

Therefore:

```text
linear.x
linear.y
linear.z

angular.x
angular.y
angular.z
```

For a differential-drive/mobile robot, `linear.x` and `angular.z` are commonly the important velocity components.

---

# 5.5 Observe Topic Data

```bash
ros2 topic echo /turtle1/pose
```

Move the turtle.

You will see:

```text
x
y
theta
linear_velocity
angular_velocity
```

### Important idea

The turtle is continuously publishing its pose.

Another node can subscribe to that data.

---

# 6. Publishing to a Topic

You can publish directly from the terminal.

```bash
ros2 topic pub \
/turtle1/cmd_vel \
geometry_msgs/msg/Twist \
"{linear: {x: 2.0}, angular: {z: 0.0}}"
```

The turtle should move forward.

---

## Continuous Publishing

```bash
ros2 topic pub --rate 10 \
/turtle1/cmd_vel \
geometry_msgs/msg/Twist \
"{linear: {x: 1.0}, angular: {z: 1.0}}"
```

The turtle should move in a curved path.

Stop:

```text
Ctrl + C
```

---

# 🧪 Challenge 1 — Draw a Square

Try to make the turtle draw:

```text
┌──────────┐
│          │
│          │
│          │
└──────────┘
```

Think about:

```text
linear.x
```

and:

```text
angular.z
```

---

# 7. Services

A service is used for a request/response interaction.

```text
CLIENT
   │
   │ Request
   ▼
SERVER
   │
   │ Response
   ▼
CLIENT
```

Examples:

```text
/reset
/spawn
/clear
```

---

# 7.1 List Services

```bash
ros2 service list
```

---

# 7.2 Check Service Type

```bash
ros2 service type /reset
```

Expected:

```text
std_srvs/srv/Empty
```

---

# 7.3 Inspect Service

```bash
ros2 interface show std_srvs/srv/Empty
```

---

# 7.4 Call Service

```bash
ros2 service call /reset std_srvs/srv/Empty
```

The turtle should return to its initial state.

---

# 7.5 Spawn Another Turtle

Check:

```bash
ros2 service type /spawn
```

Inspect:

```bash
ros2 interface show turtlesim/srv/Spawn
```

Call:

```bash
ros2 service call /spawn \
turtlesim/srv/Spawn \
"{x: 5.0, y: 5.0, theta: 0.0, name: 'turtle2'}"
```

---

# Topic vs Service

| Topic                    | Service             |
| ------------------------ | ------------------- |
| Continuous communication | Request/response    |
| Publisher/subscriber     | Client/server       |
| `/scan`                  | `/reset`            |
| `/cmd_vel`               | `/spawn`            |
| Sensor streams           | Specific operations |

---

# 8. Parameters

Parameters are configuration values associated with nodes.

---

## List Parameters

```bash
ros2 param list
```

Or:

```bash
ros2 param list /turtlesim
```

---

## Get Parameter

```bash
ros2 param get /turtlesim background_r
```

Try:

```bash
ros2 param get /turtlesim background_g
```

```bash
ros2 param get /turtlesim background_b
```

---

## Set Parameter

```bash
ros2 param set /turtlesim background_r 255
```

---

## Dump Parameters

```bash
ros2 param dump /turtlesim
```

---

# Real Robot Parameter Examples

Real robots may use parameters such as:

```text
maximum_velocity
lidar_range
camera_fps
robot_name
controller_gain
wheel_radius
wheel_separation
```

---

# 9. Actions

Actions are designed for longer-running operations.

Example:

```text
Navigation Goal
       ↓
Robot starts moving
       ↓
Feedback
       ↓
Robot reaches goal
       ↓
Result
```

---

## List Actions

```bash
ros2 action list
```

---

## Inspect Turtle Action

```bash
ros2 action info /turtle1/rotate_absolute
```

Inspect:

```bash
ros2 interface show turtlesim/action/RotateAbsolute
```

### Remember

```text
Topic
→ continuous data

Service
→ request / response

Action
→ goal / feedback / result
```

Navigation systems such as Nav2 make extensive use of action-based interfaces.

---

# 10. Workspaces, Packages and colcon

A ROS 2 workspace is a development environment containing ROS packages.

Typical structure:

```text
ros2_ws/
│
├── src/
│
├── build/
│
├── install/
│
└── log/
```

---

# 10.1 Create Workspace

```bash
mkdir -p ~/ros2_ws/src
```

```bash
cd ~/ros2_ws
```

---

# 10.2 Create Package

```bash
cd ~/ros2_ws/src
```

```bash
ros2 pkg create \
--build-type ament_python \
my_robot
```

---

# 10.3 Build Workspace

```bash
cd ~/ros2_ws
colcon build
```

---

# 10.4 Source Workspace

```bash
source install/setup.bash
```

---

# 10.5 Check Package

```bash
ros2 pkg list | grep my_robot
```

---

# What is colcon?

Think:

```text
ROS source code
       ↓
    colcon
       ↓
    Build
       ↓
build/
install/
log/
```

`colcon` is the build tool used to build ROS 2 workspaces.

---

# 10.6 Build With Symlink Install

For Python development:

```bash
colcon build --symlink-install
```

This is particularly convenient while developing Python packages because source changes can be reflected without repeatedly copying Python files into the install tree.

---

# 11. ROS 2 Debugging

One of the most important workshop skills.

If something is not working:

```text
Something doesn't work
        ↓
Is the node running?
        ↓
ros2 node list
        ↓
Does the topic exist?
        ↓
ros2 topic list
        ↓
Is someone publishing?
        ↓
ros2 topic info
        ↓
Is data arriving?
        ↓
ros2 topic echo
        ↓
Is the message type correct?
        ↓
ros2 topic type
```

---

# Essential Debugging Commands

## Nodes

```bash
ros2 node list
```

```bash
ros2 node info <node>
```

---

## Topics

```bash
ros2 topic list
```

```bash
ros2 topic info <topic>
```

```bash
ros2 topic type <topic>
```

```bash
ros2 topic echo <topic>
```

```bash
ros2 topic hz <topic>
```

---

## Services

```bash
ros2 service list
```

```bash
ros2 service type <service>
```

---

## Parameters

```bash
ros2 param list
```

```bash
ros2 param get <node> <parameter>
```

```bash
ros2 param set <node> <parameter> <value>
```

---

## Actions

```bash
ros2 action list
```

```bash
ros2 action info <action>
```

---

# 🧪 DAY 1 CHALLENGE

Without following the instructor:

1. Start turtlesim.
2. Start teleoperation.
3. Find all nodes.
4. Find all topics.
5. Find `/turtle1/cmd_vel`.
6. Find its message type.
7. Echo `/turtle1/pose`.
8. Publish velocity manually.
9. Reset the turtle.
10. Spawn another turtle.
11. Inspect parameters.
12. Create a workspace.
13. Create a package.
14. Build it with `colcon`.

---

# 🟩 DAY 2 — ROS 2 PROGRAMMING, TURTLEBOT3 & SLAM

---

# 13. Create Your First Python ROS 2 Node

We will now move from CLI commands to actual ROS 2 programming.

Architecture:

```text
/turtle1/pose
      │
      ▼
┌───────────────────┐
│ Turtle Controller │
│                   │
│ Read pose         │
│ Calculate         │
│ Publish velocity  │
└─────────┬─────────┘
          │
          ▼
/turtle1/cmd_vel
```

---

# 13.1 Create Package

```bash
cd ~/ros2_ws/src
```

```bash
ros2 pkg create \
--build-type ament_python \
turtle_controller \
--dependencies rclpy geometry_msgs turtlesim
```

---

# 13.2 Create Python Node

Create:

```text
~/ros2_ws/src/turtle_controller/
└── turtle_controller/
    └── controller.py
```

Use:

```python
import rclpy
from rclpy.node import Node

from geometry_msgs.msg import Twist
from turtlesim.msg import Pose


class TurtleController(Node):

    def __init__(self):

        super().__init__('turtle_controller')

        self.publisher = self.create_publisher(
            Twist,
            '/turtle1/cmd_vel',
            10
        )

        self.subscription = self.create_subscription(
            Pose,
            '/turtle1/pose',
            self.pose_callback,
            10
        )

    def pose_callback(self, msg):

        self.get_logger().info(
            f'x={msg.x:.2f}, y={msg.y:.2f}'
        )

        cmd = Twist()

        cmd.linear.x = 0.5

        self.publisher.publish(cmd)


def main(args=None):

    rclpy.init(args=args)

    node = TurtleController()

    rclpy.spin(node)

    node.destroy_node()

    rclpy.shutdown()


if __name__ == '__main__':
    main()
```

---

# 13.3 Understand the Code

## Node

```python
class TurtleController(Node):
```

Creates a ROS 2 node.

---

## Publisher

```python
self.create_publisher(
    Twist,
    '/turtle1/cmd_vel',
    10
)
```

Creates a publisher.

---

## Subscriber

```python
self.create_subscription(
    Pose,
    '/turtle1/pose',
    self.pose_callback,
    10
)
```

Creates a subscriber.

---

## Callback

```python
def pose_callback(self, msg):
```

Runs when a pose message arrives.

---

## Publish

```python
self.publisher.publish(cmd)
```

Publishes the velocity command.

---

# 13.4 Add Executable

Open:

```text
setup.py
```

Add:

```python
entry_points={
    'console_scripts': [
        'controller = turtle_controller.controller:main',
    ],
},
```

---

# 13.5 Build

```bash
cd ~/ros2_ws
```

```bash
colcon build --symlink-install
```

Source:

```bash
source install/setup.bash
```

---

# 13.6 Run

Start turtlesim:

```bash
ros2 run turtlesim turtlesim_node
```

Then:

```bash
ros2 run turtle_controller controller
```

---

# 13.7 Inspect Your Node

```bash
ros2 node list
```

You should see:

```text
/turtlesim
/turtle_controller
```

Inspect:

```bash
ros2 node info /turtle_controller
```

You should see:

```text
Publisher:
    /turtle1/cmd_vel

Subscriber:
    /turtle1/pose
```

---

# 14. Publisher + Subscriber Mental Model

This is one of the most important diagrams of the workshop:

```text
              TOPIC

Publisher                  Subscriber

   Node                        Node
    │                           ▲
    │                           │
    │────── message ───────────►│
    │                           │
    ▼                           │

 /turtle1/cmd_vel        /turtle1/cmd_vel
```

ROS 2 allows these nodes to communicate without being tightly coupled to each other's internal implementation.

---

# 15. Basic Robot Control

Now introduce simple robotics mathematics.

Suppose:

```text
Target:

x = 8
y = 8
```

Robot:

```text
current_x
current_y
current_theta
```

Calculate:

```text
error_x = target_x - current_x

error_y = target_y - current_y
```

Distance:

```text
distance = sqrt(error_x² + error_y²)
```

Target direction:

```text
target_angle = atan2(error_y, error_x)
```

Angular error:

```text
angle_error = target_angle - current_theta
```

Simple proportional control:

```text
linear_velocity =
    Kp × distance

angular_velocity =
    Kp × angle_error
```

---

# 🧪 Challenge 2 — Autonomous Turtle

Modify your node so that the turtle moves toward:

```text
x = 8
y = 8
```

Then try:

```text
x = 2
y = 8
```

Then:

```text
x = 8
y = 2
```

---

# 16. TurtleBot3

Now we transition from:

```text
Educational simulation
```

to:

```text
Mobile robotics simulation
```

TurtleBot3 is a compact mobile robot platform used extensively for ROS education and development.

---

# 16.1 TurtleBot3 Environment

Set the robot model:

```bash
export TURTLEBOT3_MODEL=burger
```

Check:

```bash
echo $TURTLEBOT3_MODEL
```

Expected:

```text
burger
```

To make it permanent:

```bash
echo 'export TURTLEBOT3_MODEL=burger' >> ~/.bashrc
```

---

# 17. Gazebo Simulation

Gazebo provides the simulated robotics environment.

Conceptually:

```text
ROS 2
  │
  ├── Robot
  ├── Sensors
  ├── Motors
  └── Environment
          │
          ▼
       Gazebo
```

---

# 17.1 Launch TurtleBot3 World

First:

```bash
source /opt/ros/humble/setup.bash
```

Then:

```bash
source ~/turtlebot3_ws/install/setup.bash
```

Set:

```bash
export TURTLEBOT3_MODEL=burger
```

Launch:

```bash
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
```

---

# 17.2 Teleoperate TurtleBot3

Open another terminal:

```bash
source /opt/ros/humble/setup.bash
```

```bash
source ~/turtlebot3_ws/install/setup.bash
```

```bash
export TURTLEBOT3_MODEL=burger
```

Run:

```bash
ros2 run turtlebot3_teleop teleop_keyboard
```

Drive the robot.

---

# 17.3 Inspect Robot Nodes

```bash
ros2 node list
```

---

# 17.4 Inspect Topics

```bash
ros2 topic list
```

Important topics include:

```text
/cmd_vel
/odom
/scan
/tf
/tf_static
```

---

# 17.5 Inspect `/cmd_vel`

```bash
ros2 topic info /cmd_vel
```

```bash
ros2 topic type /cmd_vel
```

Expected:

```text
geometry_msgs/msg/Twist
```

---

# 18. RViz2

RViz2 is used to visualize ROS data.

It can display:

* Robot model
* LiDAR
* Map
* TF
* Odometry
* Paths
* Sensors

---

# 18.1 Launch RViz2

```bash
ros2 launch turtlebot3_bringup rviz2.launch.py
```

---

# 19. TF — Coordinate Frames

Robots contain many coordinate systems.

Example:

```text
map
 │
 ▼
odom
 │
 ▼
base_footprint
 │
 ▼
base_link
 │
 ▼
laser
```

---

## Meaning

### `map`

Global map coordinate system.

### `odom`

Odometry reference.

### `base_link`

Robot body frame.

### `laser`

LiDAR sensor frame.

---

# 19.1 Inspect TF

```bash
ros2 topic echo /tf
```

Static transforms:

```bash
ros2 topic echo /tf_static
```

---

# Key Concept

TF answers:

> **Where is coordinate frame A relative to coordinate frame B?**

This becomes critical for:

```text
SLAM
Localization
Navigation
Manipulation
Computer Vision
Sensor Fusion
```

---

# 20. LiDAR and LaserScan

TurtleBot3 uses a 2-D laser scanner for distance measurements around the robot. ROBOTIS describes its LDS sensors as 360° laser scanners used for SLAM and navigation.

Conceptually:

```text
              WALL
        █████████████

             ↑
        \    │    /
         \   │   /
          \  │  /
           \ │ /
            \│/
             🤖
```

The LiDAR produces distance measurements.

---

# 20.1 Inspect `/scan`

```bash
ros2 topic info /scan
```

Type:

```bash
ros2 topic type /scan
```

Expected:

```text
sensor_msgs/msg/LaserScan
```

---

# 20.2 View LiDAR Data

```bash
ros2 topic echo /scan
```

You will see fields including:

```text
angle_min
angle_max
angle_increment
range_min
range_max
ranges
```

---

# 20.3 Understand `ranges`

The `ranges` array contains measured distances.

Conceptually:

```text
ranges[0]
ranges[1]
ranges[2]
...
ranges[n]
```

Each measurement corresponds to an angle.

This is the raw information SLAM can use to understand the environment.

---

# 21. SLAM

## What does SLAM mean?

```text
S
Simultaneous

L
Localization

A
And

M
Mapping
```

The robot wants to estimate:

```text
Where am I?
```

while simultaneously building:

```text
What does the environment look like?
```

---

# 21.1 SLAM Inputs

A simplified system:

```text
LiDAR
  │
  ▼
/scan
  │
  ├─────────────┐
  │             │
  ▼             ▼
SLAM         Odometry
  │             │
  └──────┬──────┘
         ▼
      SLAM
         │
     ┌───┴────┐
     ▼        ▼
   /map      /tf
```

---

# 21.2 Why Odometry Matters

Odometry provides an estimate of how the robot moved.

For example:

```text
Start
  ↓
Move 1 m
  ↓
Rotate
  ↓
Move 2 m
```

Odometry estimates the robot's movement.

LiDAR provides environmental observations.

SLAM combines these sources to estimate the robot's trajectory and construct a map.

---

# 21.3 Run TurtleBot3 World

```bash
export TURTLEBOT3_MODEL=burger
```

```bash
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
```

---

# 21.4 Launch SLAM

Open another terminal:

```bash
source /opt/ros/humble/setup.bash
```

```bash
source ~/turtlebot3_ws/install/setup.bash
```

```bash
export TURTLEBOT3_MODEL=burger
```

Run:

```bash
ros2 launch turtlebot3_cartographer cartographer.launch.py use_sim_time:=True
```

---

# 21.5 Start Teleoperation

```bash
export TURTLEBOT3_MODEL=burger
```

```bash
ros2 run turtlebot3_teleop teleop_keyboard
```

Move the robot slowly around the environment.

---

# 21.6 Observe the Map

In RViz2 you should see:

```text
Robot
   ↓
LiDAR observations
   ↓
Walls
   ↓
Map
```

Move around the environment systematically.

Avoid moving too quickly.

---

# 21.7 Inspect SLAM Topics

```bash
ros2 topic list
```

Look for:

```text
/map
/scan
/odom
/tf
```

---

# 21.8 Inspect Map

```bash
ros2 topic info /map
```

Type:

```bash
ros2 topic type /map
```

Expected:

```text
nav_msgs/msg/OccupancyGrid
```

---

# 21.9 Occupancy Grid

A map can conceptually be represented as:

```text
UNKNOWN UNKNOWN UNKNOWN UNKNOWN

FREE    FREE    FREE    WALL

FREE    FREE    FREE    WALL

FREE    FREE    FREE    FREE
```

Typical occupancy-grid interpretation:

```text
-1  → unknown
 0  → free
100 → occupied
```

---

# 22. Save the Map

After completing the environment scan:

```bash
ros2 run nav2_map_server map_saver_cli -f ~/my_map
```

Check:

```bash
ls ~/my_map*
```

You should have files such as:

```text
my_map.pgm
my_map.yaml
```

---

# 23. Introduction to Navigation2

SLAM creates a map.

Navigation uses that map to help a robot move autonomously.

Conceptually:

```text
                 MAP
                  │
                  ▼
             Localization
                  │
                  ▼
              Navigation
                  │
           ┌──────┴──────┐
           ▼             ▼
     Path Planning   Obstacle Avoidance
           │             │
           └──────┬──────┘
                  ▼
               /cmd_vel
                  │
                  ▼
                Robot
```

---

# 23.1 Navigation Goal

A navigation system can receive a goal:

```text
Goal:
X = 3.0
Y = 2.0
```

Then:

```text
Robot
  ↓
Plan path
  ↓
Avoid obstacles
  ↓
Follow path
  ↓
Reach goal
```

---

# 23.2 Launch Navigation

First launch Gazebo:

```bash
export TURTLEBOT3_MODEL=burger
```

```bash
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
```

Then:

```bash
export TURTLEBOT3_MODEL=burger
```

```bash
ros2 launch turtlebot3_navigation2 navigation2.launch.py \
use_sim_time:=True \
map:=$HOME/my_map.yaml
```

Then use RViz2 to:

```text
1. Set initial pose
2. Set navigation goal
3. Observe path planning
4. Observe robot movement
```

---

# 🧪 24. FINAL PROJECT

## Mission

Your team must demonstrate an autonomous robotics workflow.

### Level 1 — ROS 2

Launch ROS 2.

### Level 2 — Nodes

Show:

```bash
ros2 node list
```

### Level 3 — Topics

Show:

```bash
ros2 topic list
```

### Level 4 — Communication

Show:

```text
/cmd_vel
/scan
/odom
```

### Level 5 — Sensor

Demonstrate:

```bash
ros2 topic echo /scan
```

### Level 6 — Visualization

Open RViz2.

### Level 7 — SLAM

Build a map.

### Level 8 — Save Map

```bash
ros2 run nav2_map_server map_saver_cli -f ~/my_map
```

### Level 9 — Navigation

Load the map.

### Level 10 — Autonomous Goal

Give the robot a navigation goal.

---

# 🧠 FINAL ROS 2 MENTAL MODEL

You should now understand:

```text
                         ROS 2
                           │
          ┌────────────────┼────────────────┐
          │                │                │
        Nodes            Topics          Services
          │                │                │
          │                │                │
          └────────────────┼────────────────┘
                           │
                        Messages
                           │
                       Parameters
                           │
                         Actions
                           │
                           ▼
                        Robot
                           │
          ┌────────────────┼────────────────┐
          │                │                │
        Sensors          Compute         Actuators
          │                │                │
        LiDAR             SLAM            Motors
        Camera            Nav2            Wheels
        IMU               AI
```

---

# ⚡ ROS 2 COMMAND CHEAT SHEET

## Environment

```bash
source /opt/ros/humble/setup.bash
```

```bash
printenv | grep ROS
```

---

## Nodes

```bash
ros2 node list
```

```bash
ros2 node info <node>
```

---

## Topics

```bash
ros2 topic list
```

```bash
ros2 topic info <topic>
```

```bash
ros2 topic type <topic>
```

```bash
ros2 topic echo <topic>
```

```bash
ros2 topic hz <topic>
```

```bash
ros2 topic pub <topic> <type> <data>
```

---

## Services

```bash
ros2 service list
```

```bash
ros2 service type <service>
```

```bash
ros2 service call <service> <type> <data>
```

---

## Actions

```bash
ros2 action list
```

```bash
ros2 action info <action>
```

---

## Parameters

```bash
ros2 param list
```

```bash
ros2 param get <node> <parameter>
```

```bash
ros2 param set <node> <parameter> <value>
```

```bash
ros2 param dump <node>
```

---

## Packages

```bash
ros2 pkg list
```

```bash
ros2 pkg executables
```

```bash
ros2 pkg prefix <package>
```

---

## Interfaces

```bash
ros2 interface list
```

```bash
ros2 interface show <interface>
```

---

## Workspace

```bash
mkdir -p ~/ros2_ws/src
```

```bash
cd ~/ros2_ws
```

```bash
colcon build
```

```bash
colcon build --symlink-install
```

```bash
source install/setup.bash
```

---

# 🔍 ROS 2 DEBUGGING FLOWCHART

```text
                Something is not working
                         │
                         ▼
                 Is ROS sourced?
                         │
                         ▼
                ros2 --help
                         │
                         ▼
                  Node running?
                         │
                  ros2 node list
                         │
                         ▼
                  Topic exists?
                         │
                 ros2 topic list
                         │
                         ▼
               Correct publisher?
                         │
                 ros2 topic info
                         │
                         ▼
                  Data arriving?
                         │
                 ros2 topic echo
                         │
                         ▼
                Correct data type?
                         │
                 ros2 topic type
                         │
                         ▼
                    Debug
```

---

# 🛠 Troubleshooting

## Problem: `ros2: command not found`

Run:

```bash
source /opt/ros/humble/setup.bash
```

If it works, add it permanently:

```bash
echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
```

---

# Problem: Package not found

Example:

```text
Package 'turtlesim' not found
```

Check:

```bash
source /opt/ros/humble/setup.bash
```

Then:

```bash
ros2 pkg list | grep turtlesim
```

---

# Problem: Custom package not found

Source the workspace:

```bash
source ~/ros2_ws/install/setup.bash
```

Then:

```bash
ros2 pkg list | grep turtle_controller
```

---

# Problem: Changes to Python code are not reflected

Build:

```bash
colcon build --symlink-install
```

Then:

```bash
source install/setup.bash
```

---

# Problem: Gazebo is slow

Try:

* Close Chrome tabs.
* Close unnecessary applications.
* Reduce Gazebo rendering load.
* Use a machine with adequate RAM/GPU.
* Run fewer visualization tools simultaneously.

---

# Problem: TurtleBot3 model missing

Check:

```bash
echo $TURTLEBOT3_MODEL
```

Set:

```bash
export TURTLEBOT3_MODEL=burger
```

---

# Problem: ROS nodes cannot see each other

Check:

```bash
printenv | grep ROS
```

Check:

```bash
echo $ROS_DOMAIN_ID
```

For a classroom, ensure students who need to communicate are using the same ROS domain.

---

# Problem: Gazebo launches but robot is missing

Check:

```bash
echo $TURTLEBOT3_MODEL
```

Then:

```bash
source /opt/ros/humble/setup.bash
source ~/turtlebot3_ws/install/setup.bash
```

Try launching again.

---

# 📖 CONCEPT SUMMARY

| Concept    | Meaning                       | Example             |
| ---------- | ----------------------------- | ------------------- |
| Node       | Running ROS 2 process         | `turtlesim`         |
| Topic      | Communication stream          | `/scan`             |
| Publisher  | Sends topic messages          | LiDAR               |
| Subscriber | Receives topic messages       | SLAM                |
| Message    | Data structure                | `LaserScan`         |
| Service    | Request/response              | `/reset`            |
| Action     | Long-running goal             | Navigation          |
| Parameter  | Configuration value           | Speed               |
| Package    | ROS software unit             | `turtlesim`         |
| Workspace  | Development environment       | `ros2_ws`           |
| colcon     | Build system/tool             | `colcon build`      |
| TF         | Coordinate-frame relationship | `base_link → laser` |
| Odometry   | Estimated movement            | `/odom`             |
| LiDAR      | Distance sensor               | `/scan`             |
| SLAM       | Mapping + localization        | Cartographer        |
| RViz2      | Visualization tool            | Map/LiDAR           |
| Gazebo     | Simulation environment        | TurtleBot3          |
| Nav2       | Navigation framework          | Goal → path         |

---

# 🔗 HOW EVERYTHING CONNECTS

This is the complete robotics pipeline:

```text
                    ROBOT

              ┌─────────────┐
              │   Sensors   │
              └──────┬──────┘
                     │
          ┌──────────┼──────────┐
          ▼          ▼          ▼
        LiDAR       IMU       Camera
          │          │          │
          └──────────┼──────────┘
                     │
                     ▼
                   ROS 2
                     │
             ┌───────┴───────┐
             ▼               ▼
            SLAM           Perception
             │               │
             ▼               ▼
            Map              AI
             │
             ▼
        Localization
             │
             ▼
            Nav2
             │
             ▼
       Path Planning
             │
             ▼
       Motion Control
             │
             ▼
          /cmd_vel
             │
             ▼
           Motors
```

---

# 🚀 WHAT TO LEARN NEXT

After completing this workshop, continue in this order:

```text
1. ROS 2 Fundamentals
        ↓
2. Python ROS 2
        ↓
3. TF2
        ↓
4. URDF
        ↓
5. Xacro
        ↓
6. ros2_control
        ↓
7. Gazebo
        ↓
8. SLAM
        ↓
9. Localization
        ↓
10. Nav2
        ↓
11. Computer Vision
        ↓
12. OpenCV
        ↓
13. Robot Manipulation
        ↓
14. MoveIt 2
        ↓
15. Sensor Fusion
        ↓
16. AI + Robotics
        ↓
17. Industrial Robotics
```

---

# 🏭 INDUSTRIAL ROS 2 CONNECTION

The concepts learned here are directly useful when working with industrial/mobile robotic systems.

A simplified industrial architecture may look like:

```text
                  WMS
                   │
                   ▼
                  WCS
                   │
                   ▼
              Robot Fleet
                   │
          ┌────────┼────────┐
          ▼        ▼        ▼
        AMR 1    AMR 2    AMR 3
          │        │        │
         ROS 2    ROS 2    ROS 2
          │        │        │
        LiDAR    LiDAR    LiDAR
        SLAM     SLAM     SLAM
        Nav2     Nav2     Nav2
```

Understanding:

```text
Nodes
Topics
Services
Actions
Parameters
TF
SLAM
Navigation
```

provides the foundation for understanding much larger robotics software architectures.

---

# 🎯 FINAL WORKSHOP CHECKLIST

Before completing the workshop, verify that you can answer **YES** to all of these:

* [ ] I can explain ROS 2.
* [ ] I understand nodes.
* [ ] I can list nodes.
* [ ] I can inspect a node.
* [ ] I understand topics.
* [ ] I can list topics.
* [ ] I can inspect topic data.
* [ ] I can identify a message type.
* [ ] I can publish a message.
* [ ] I understand services.
* [ ] I can call a service.
* [ ] I understand parameters.
* [ ] I can get/set parameters.
* [ ] I understand actions.
* [ ] I understand packages.
* [ ] I can create a workspace.
* [ ] I can create a package.
* [ ] I can use `colcon`.
* [ ] I can create a Python ROS 2 node.
* [ ] I understand publishers/subscribers.
* [ ] I understand `/cmd_vel`.
* [ ] I understand `/odom`.
* [ ] I understand `/scan`.
* [ ] I understand TF.
* [ ] I understand RViz2.
* [ ] I understand Gazebo.
* [ ] I understand LiDAR.
* [ ] I understand SLAM.
* [ ] I can generate a map.
* [ ] I can save a map.
* [ ] I understand the purpose of Nav2.

---

# 🧑‍🏫 INSTRUCTOR TEACHING RULE

Do not teach ROS 2 as a collection of commands.

For every command ask:

### 1. What is this?

### 2. Why do we need it?

### 3. What is happening internally?

### 4. What output should we expect?

### 5. How can we inspect it?

### 6. What happens if we modify it?

### 7. How is this used on a real robot?

For example:

```bash
ros2 topic echo /scan
```

Don't stop at:

> "This shows LiDAR data."

Explain:

```text
LiDAR
 ↓
Driver
 ↓
ROS 2 Node
 ↓
/scan
 ↓
LaserScan message
 ↓
SLAM
 ↓
Map
 ↓
Navigation
```

That connection is what turns the workshop from a **ROS command tutorial into a robotics engineering workshop**.

---

# 📚 OFFICIAL RESOURCES

## ROS 2

* [ROS 2 Documentation](https://docs.ros.org/en/humble/)
* [ROS 2 Tutorials](https://docs.ros.org/en/humble/Tutorials.html)

## TurtleBot3

* [TurtleBot3 e-Manual](https://emanual.robotis.com/docs/en/platform/turtlebot3/)
* [TurtleBot3 Simulation](https://emanual.robotis.com/docs/en/platform/turtlebot3/simulation/)
* [TurtleBot3 SLAM](https://emanual.robotis.com/docs/en/platform/turtlebot3/slam_simulation/)
* [TurtleBot3 Navigation](https://emanual.robotis.com/docs/en/platform/turtlebot3/nav_simulation/)

## ROS 2 Packages

* [ROS 2 GitHub](https://github.com/ros2)
* [TurtleBot3 GitHub](https://github.com/ROBOTIS-GIT/turtlebot3)
* [TurtleBot3 Simulation GitHub](https://github.com/ROBOTIS-GIT/turtlebot3_simulations)

---

# 📌 Important Note About ROS 2 Distributions

This workshop is written primarily for:

```text
Ubuntu 22.04
ROS 2 Humble
```

ROS 2 commands and TurtleBot3 package workflows can differ between ROS distributions.

If you use another ROS 2 distribution, verify the corresponding official documentation before copying commands directly.

---

# 🏁 Workshop Completion

If you successfully completed this workshop, you have gone from:

```text
"I don't know ROS 2"
```

to:

```text
ROS 2
 │
 ├── Nodes
 ├── Topics
 ├── Services
 ├── Actions
 ├── Parameters
 ├── Messages
 ├── Packages
 ├── colcon
 │
 ├── Python Nodes
 │
 ├── TurtleBot3
 ├── Gazebo
 ├── RViz2
 ├── TF
 ├── LiDAR
 │
 ├── SLAM
 ├── Mapping
 │
 └── Navigation
```

And most importantly:

> **You now have the foundation to start building real ROS 2 robotic systems.**

---

## ⭐ If this workshop helped you

Consider giving the repository a ⭐ on GitHub and contributing improvements, examples and new practical exercises.

**Happy Robotics! 🤖**
