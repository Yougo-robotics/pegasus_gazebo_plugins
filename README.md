# pegasus_gazebo_plugins

## Overview
This is a ROS package developed for our quadruped robot "pegasus" gazebo_plugin ,closed_loop_plugin is one of the plugins only announced here,to solve the issuethat URDF not support Closed loop chains 

*Author: Angel_jj
<br>*Department ：The Chinese University of Hong Kong,Shenzhen，IRIM(Institute of Robotics and Intelligent Manufacturing)
<br>*Maintainer: Angel_jj, 522483402@.qqcom

## Introduction

[Tutorial: Using a URDF in Gazebo ](http://gazebosim.org/tutorials?tut=ros_urdf&cat=connect_ros).

The Universal Robotic Description Format (URDF) is an XML file format used in ROS to describe all elements of a robot. To use a URDF file in Gazebo, some additional simulation-specific tags must be added to work properly with Gazebo. This tutorial explains the necessary steps to successfully use your URDF-based robot in Gazebo, saving you from having to create a separate SDF file from scratch and duplicating description formats. Under the hood, Gazebo will then convert the URDF to SDF automatically.

Background
While URDFs are a useful and standardized format in ROS, they are lacking many features and have not been updated to deal with the evolving needs of robotics. URDF can only specify the kinematic and dynamic properties of a single robot in isolation. URDF can not specify the pose of the robot itself within a world. It is also not a universal description format since it cannot specify joint loops (parallel linkages), and it lacks friction and other properties. Additionally, it cannot specify things that are not robots, such as lights, heightmaps, etc.

On the implementation side, the URDF syntax breaks proper formatting with heavy use of XML attributes, which in turn makes URDF more inflexible. There is also no mechanism for backward compatibility.

To deal with this issue, a new format called the Simulation Description Format (SDF) was created for use in Gazebo to solve the shortcomings of URDF. SDF is a complete description for everything from the world level down to the robot level. It is scalable, and makes it easy to add and modify elements. The SDF format is itself described using XML, which facilitates a simple upgrade tool to migrate old versions to new versions. It is also self-descriptive.

It is the intention of this author to make URDFs as fully documented and supported in Gazebo as possible, but it is relevant to the reader to understand why the two formats exist and the shortcomings of both. It would be nice if more work was put into URDFs to update them to the current needs of robotics.

#### Summary：
The URDF served the ROS, it has several notable shortcomings.one is it does not support closed loop chains.
The SDF served the gazebo, support closed loop chains - this can be achieved by allowing two different joints to have the same child link but different parents
The closed_loop_plugin works after the robot model is converted from urdf to sdf, inserting a new joint into the sdf file of the robot model.
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
#### exmaple:
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
#### note：
You can change the position where two joints are connected in closed_loop_plugin.cpp

```cpp
math::Pose jointOrigin(0.00,0.00,0.00,0.00,-0.00,0.00);
```
math::Pose jointOrigin(x,y,z,roll,pitch,yaw);

## Bugs & Feature Requests
Please report bugs and request features using the [Issue Tracker](https://github.com/wojiaojiao/pegasus_gazebo_plugins/issues).


