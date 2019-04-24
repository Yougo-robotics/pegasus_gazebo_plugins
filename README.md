# pegasus_gazebo_plugins

## Overview
This is a ROS package developed for our quadruped robot "pegasus" gazebo_plugin ,closed_loop_plugin is one of the plugins only announced here,to solve the issuethat URDF not support Closed loop chains 

*Author: Angel_jj
<br>*Department ：The Chinese University of Hong Kong,Shenzhen，IRIM(Institute of Robotics and Intelligent Manufacturing)
<br>*Maintainer: Angel_jj, 522483402@.qqcom

## Introduction

The URDF (Universal Robot Description Format) served the ROS, it has several notable shortcomings.one is it does not support closed loop chains.

The SDF (Simulation Description Format) served the gazebo, support closed loop chains - this can be achieved by allowing two different joints to have the same child link but different parents
<br>relationship here：
<br>![](https://github.com/wojiaojiao/pegasus_gazebo_plugins/raw/master/doc/diagram2.png) 
## Building
In order to install the pegasus_gazebo_plugins, clone the latest version from this repository into your catkin workspace and compile the package using ROS.

<br>cd catkin_workspace/src
<br>git clone https://github.com/wojiaojiao/pegasus_gazebo_plugins.git
<br>cd ../
<br>catkin_make

## Usage
This closed_loop_plugin just like a button that connects two joints,
<br>\<joint> the name of the added joint
<br>\<child> the name of child coordinate that added joint
<br>\<parent> the name of parent coordinate that added joint

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
The following is a four-link closed-loop chain
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
You can change the position where two joints are connected in closed_loop_plugin.cpp

```cpp
math::Pose jointOrigin(0.00,0.00,0.00,0.00,-0.00,0.00);
```
math::Pose jointOrigin(x,y,z,roll,pitch,yaw);

## Bugs & Feature Requests
Please report bugs and request features using the [Issue Tracker](https://github.com/wojiaojiao/pegasus_gazebo_plugins/issues).


