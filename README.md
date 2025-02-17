# Hand-eye calibration for eye-on-hand and eye-on-base
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
