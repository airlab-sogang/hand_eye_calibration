# Hand-eye calibration for eye-on-hand and eye-on-base
---
## References
 * https://github.com/IFL-CAMP/easy_handeye.git
 * https://github.com/pal-robotics/aruco_ros.git
---
Tested environment : Ubuntu 20.04 & ROS1 noetic
---
## Functions
1. Aruco marker detection
2. Hand-eye calibration
  * Eye-on-base
  * Eye-on-hand
---
## Aruco marker detection
* Aruco marker customizer : https://chev.me/arucogen/
  * You should set **Dictionary** to **Original ArUco**
### Usage (after building this package)
 ```
 roscd aruco_ros
 cd launch
 nano single.launch
 ```
Set **markerId** and **markerSize** to the custormized value.

Then execute your camera launch file and aruco detection launch file.
```
roslaunch realsense2_camera rs_multiple_devices.launch serial_no_camera1:={serial number} serial_no_camera2:={serial number}
roslaunch aruco_ros single.launch camera:={camera_name}
```
After that, you can verify the transformation from the camera to the aruco marker through topic.
---
## Hand-eye calibration
* If you need the function to calibrate cameras, you don't need to execute upper launch files.
* When you calibrate eye-on-base camera, you should attach an aruco marker in a fixed pose relative to the robot base. Otherwise, you should place it in a fixed pose relative to the end effector of robot.

1. Edit the calibration launch file in consideration of camera name and frame name.
```
roscd easy_handeye
cd launch
nano hand_eye_calibration.launch
```
You should set the camera names, **robot_base_frame**, and **robot_effector_frame** properly.

2. Execute a robot launch file and camera launch file.
```
roslaunch ur5_e_moveit_config ur5_e_moveit_planning_execution.launch
roslaunch realsense2_camera rs_multiple_devices.launch serial_no_camera1:={serial number} serial_no_camera2:={serial number}
```

3. Execute the calibration launch file whose **eye_on_hand** arguement should be set to 'true' or 'false'.
```
roslaunch easy_handeye hand_eye_calibration.launch eye_on_hand:={type}
```
4. Then you can see a GUI for calibration. You can take samples to press **Take Sample** button in different poses, and calculate the tranformation by the button **Compute**. You can select the calibration algorithms in **Calibration algorithm**. The following tips for accuracy are
   * Maximize rotation between poses.
   * Minimize the distance from the target to the camera of the tracking system.
   * Minimize the translation between poses.
   * Use redundant poses.
   * Calibrate the camera intrinsics if necessary / applicable.
   * Calibrate the robot if necessary / applicable.
