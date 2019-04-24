# pegasus_gazebo_plugins

## Overview
This is a gazebo_plugin ROS package developed for our quadruped robot "pegasus",closed_loop_plugin is to solve only one of the plugins is announced here,to solve the problem that URDF not support Closed loop chains 

*Author: Angel_jj
<br>*Department ：The Chinese University of Hong Kong,Shenzhen，IRIM(Institute of Robotics and Intelligent Manufacturing)
<br>*Maintainer: Angel_jj, 522483402@.qqcom
<br>Introduction

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

## Building
In order to install the pegasus_gazebo_plugins, clone the latest version from this repository into your catkin workspace and compile the package using ROS.

<br>cd catkin_workspace/src
<br>git clone https://github.com/wojiaojiao/pegasus_gazebo_plugins.git
<br>cd ../
<br>catkin_make

## Usage

in yours robot.urdf
add:
```XML
     <gazebo>
       <plugin name="Myrobot_ClosedLoopPlugin" filename="libpegasus_gazebo_closed_loop_plugin.so">
           <joint>lf_stick2_leg_joint</joint>
           <child>lf_leg_link</child>
           <parent>lf_stick2_link</parent>
       </plugin>
     </gazebo>
```

My example：
```XML
     <gazebo>
       <plugin name="lf_ClosedLoopPlugin" filename="libpegasus_gazebo_closed_loop_plugin.so">
           <joint>lf_stick2_leg_joint</joint>
           <child>lf_leg_link</child>
           <parent>lf_stick2_link</parent>
       </plugin>
     </gazebo>
```

## Bugs & Feature Requests
Please report bugs and request features using the [Issue Tracker](https://github.com/wojiaojiao/pegasus_gazebo_plugins/issues).


