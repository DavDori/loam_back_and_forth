# LOAM back and forth

This is a LOAM (Lidar Odometry and Mapping) ROS package for back and forth tilting 2D laser scanner. This package is a simple modified copy of the original one release by [Ji Zhang](http://www.frc.ri.cmu.edu/~jizhang03/). The only change on top of the original one is to make it a Catkin package and work under ROS Indigo. Please cite their paper if this package is used. 

Wiki Webpage by the Author: [http://wiki.ros.org/loam_back_and_forth](http://wiki.ros.org/loam_back_and_forth)

J. Zhang and S. Singh. LOAM: Lidar Odometry and Mapping in Real-time. Robotics: Science and Systems Conference (RSS). Berkeley, CA, July 2014.([PDF](http://www.frc.ri.cmu.edu/~jizhang03/Publications/RSS_2014.pdf))([VIDEO](https://www.youtube.com/watch?feature=player_embedded&v=8ezyhTAEyHs))

<a href="http://www.youtube.com/watch?feature=player_embedded&v=8ezyhTAEyHs
" target="_blank"><img src="http://img.youtube.com/vi/8ezyhTAEyHs/0.jpg" 
alt="LOAM back and forth" width="240" height="180" border="10" /></a>

# how to use

## Installation

Here I assume you have a Catkin workspace under `PATH/TO/YOUR/WORKSPACE/`.
Gitclone the package into your `src` folder:

```shell
cd PATH/TO/YOUR/WORKSPACE/src
git clone https://github.com/daobilige-su/loam_back_and_forth
```

Move to the workspace and compile the package

```shell
cd PATH/TO/YOUR/WORKSPACE/
catkin_make
source devel/setup.bash
```

Download a ROS bag file for test dataset [nsh_staircase](https://drive.google.com/file/d/1Wi34SrPrsStDSgmm9Uv4kOX4LSKRYsjk/view?usp=drive_link), which is a modified version of the original. In this version, the `frame_id` of the topics has been modified to comply with rviz outside indigo version.

## Run demo
Run the package and rosbag file:

1) in 1st terminal:

```shell
roslaunch loam_back_and_forth loam_back_and_forth.launch
```

2) in 2nd terminal (use -r 0.5 if the result look bad and it is due to the less powerful CPU, (e.g. rosbag play nsh_staircase.bag -r 0.5)):

```shell
rosbag play nsh_staircase.bag
```


3) in a 3rd terminal run rviz with the configuration file provided for the demo


YOU SHOULD SEE A RESULT SIMILAR TO THEIR DEMO VIDEO [nsh_staircase DEMO VIDEO](http://www.frc.ri.cmu.edu/~jizhang03/Videos/nsh_staircase.mp4). GOOD LUCK.

# Original Introduction by the author:

Lidar Odometry and Mapping (Loam) is a realtime method for state estimation and mapping using a 3D lidar, and optionally an IMU. The program contains four nodes. The “scanRegistration” node stacks laser scans within a sweep and publishes them as point cloud. The “laserOdometry” node estimates motion of the lidar between two sweeps, at a higher frame rate. The node corrects distortion in the point cloud from motion of the lidar. The “laserMapping” node takes the output of “laser_odometry” and incrementally builds a map. It also computes pose of the lidar on the map, at a lower frame rate. The state estimation of the lidar is combination of the outputs from “laserOdometry” and “laserMapping”, integrated in the “transformMaintenance” node. 

The program is still being tested on ROS Noetic, on a laptop computer with 2.5 GHz quad cores and 6 Gib memory (the program consumes two cores). This version uses a lidar that spins back and forth.

Wiki Webpage: http://wiki.ros.org/loam_back_and_forth

