# pegasus_gazebo_plugins

## Overview
This is a gazebo_plugin ROS package developed for our quadruped robot "pegasus",closed_loop_plugin used 

*Author: Angel_jj
<br>*Maintainer: Angel_jj, 522483402@qqcom

## Building
In order to install the pegasus_gazebo_plugins, clone the latest version from this repository into your catkin workspace and compile the package using ROS.

<br>cd catkin_workspace/src
<br>git clone https://github.com/wojiaojiao/pegasus_gazebo_plugins.git 
<br>cd ../
<br>catkin_make

## Usage

in yours robot.urdf
add:
     <gazebo>
       <plugin name="Myrobot_ClosedLoopPlugin" filename="libpegasus_gazebo_closed_loop_plugin.so">
           <joint>lf_stick2_leg_joint</joint>
           <child>lf_leg_link</child>
           <parent>lf_stick2_link</parent>
       </plugin>
     </gazebo>


My example：
     <gazebo>
       <plugin name="lf_ClosedLoopPlugin" filename="libpegasus_gazebo_closed_loop_plugin.so">
           <joint>lf_stick2_leg_joint</joint>
           <child>lf_leg_link</child>
           <parent>lf_stick2_link</parent>
       </plugin>
     </gazebo>



