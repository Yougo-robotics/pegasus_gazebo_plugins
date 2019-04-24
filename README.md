# pegasus_gazebo_plugins

## Overview
This is a ROS package developed for our quadruped robot "pegasus" gazebo_plugin ,closed_loop_plugin is one of the plugins only announced here,to solve the issuethat URDF not support Closed loop chains 

*Author: Angel_jj
<br>*Department ：The Chinese University of Hong Kong,Shenzhen，IRIM(Institute of Robotics and Intelligent Manufacturing)
<br>*Maintainer: Angel_jj, 522483402@.qqcom

## Introduction

The URDF (Universal Robot Description Format) has not been updated in quite a while. Although it has served the ROS community admirably, it has several notable shortcomings.

URDF format

Shortcomings
Closed loop chains - The URDF is not as Universal as the name implies, e.g. it does not support closed loop chains.

SDF Format

The SDF or Scene Definition Format was defined for the Gazebo simulator and has become fairly well standardized for Gazebo. 
Pros

Closed loop chains

Allow closed loop chains - this can be achieved by allowing two different joints to have the same child link but different parents
SDF supports something similar (see the PR2 gripper closed loop here).
It does not seem like this will require a syntax change.
<br>![](https://github.com/wojiaojiao/pegasus_gazebo_plugins/raw/master/doc/diagram2.png) 
## Building
In order to install the pegasus_gazebo_plugins, clone the latest version from this repository into your catkin workspace and compile the package using ROS.

<br>cd catkin_workspace/src
<br>git clone https://github.com/wojiaojiao/pegasus_gazebo_plugins.git
<br>cd ../
<br>catkin_make

## Usage
This closed_loop_plugin just like a button that connects two joints,
<br>label <joint> is like a button represents that you want to add new joints 
<br>label <child> and label <parent> represents the two joints to be connected，respectively the parent joint and the child joint of the newly added joint

<br>add to your robot.urdf：

```XML
     <gazebo>
       <plugin name="Myrobot_ClosedLoopPlugin" filename="libpegasus_gazebo_closed_loop_plugin.so">
           <joint>add_joint</joint>
           <child>add_joint_child_link</child>
           <parent>add_joint_parent_link</parent>
       </plugin>
     </gazebo>
```
### exmaple:
<br>The following is a four-link closed-loop chain
```XML
     <gazebo>
       <plugin name="Myrobot_ClosedLoopPlugin" filename="libpegasus_gazebo_closed_loop_plugin.so">
           <joint>red_green_joint</joint>
           <child>red_link</child>
           <parent>green_link</parent>
       </plugin>
     </gazebo>
```
<br>![](https://github.com/wojiaojiao/pegasus_gazebo_plugins/raw/master/doc/diagram1.png) 
### note：
<br>
You can change the position where two joints are connected in closed_loop_plugin.cpp.
```cpp
math::Pose jointOrigin(0.00,0.00,0.00,0.00,-0.00,0.00);
```
<br>math::Pose jointOrigin(x,y,z,roll,pitch,yaw);

## Bugs & Feature Requests
Please report bugs and request features using the [Issue Tracker](https://github.com/wojiaojiao/pegasus_gazebo_plugins/issues).


