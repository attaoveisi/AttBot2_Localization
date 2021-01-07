# AttBot2_Localization
The repository is a benchmark for localizing AttBot2.0 using robot_localization package. The package consists of the following main packages:

  -**Rosserial:** This is used for interfacing with an Arduino Due board which delivers the raw `/odom` and `/imu_data` messages as topic to ROS environment.
  
  
  -**Robot_localization:** This is the fusion stack that combines the measurements and delivers the filtered odometry in `robot_ekf/odom_combined` topic.
  
  
  -**hector_slam:** for SLAM purposes, and generating a map as well as the `/pose` in the map.
  
  
  -**RPLidar_ros:** this is the driver of the Lidar
  
## The localization logic:

An extended kalman filter fuses the odometry and imu data. The IMU data is measured by a Bosch BNO055 sensor while the odometry is the fused result from two motor encoders, a GY-85 (gyro, compass, imu), and an single track model.

The fusion is done in 2D.

A bag data of the measurement is available in the `measurements` folder.


## How to use:

Start a `roscore`.

Start the communication with DUE: `rosrun rosserial_python serial_node.py _baud:=57600 ...`

let the system calibrate, this may take up to 10 seconds and the calibration is over once the red LED flashes.

start the robot_localization stack: `roslaunch robot_localization ekf_imu_odometry.launch`

start the Lidar stuff:

```
roslaunch rplidar_ros rplidar.launch
roslaunch hector_slam_launch tutorial_tif.launch
```

![til](https://media.giphy.com/media/5yUlEXMS6K7d195qZ3/giphy.gif)

![til](https://giphy.com/gifs/AeeQCAKlcn99xEH6fw/html5)


