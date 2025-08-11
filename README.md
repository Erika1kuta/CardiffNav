# [CardiffNav]

## Overview

[TODO]

## Objective of the Dataset

[TODO]

## Dataset

### Sensor Setups

| Sensor                  | Specifications                                                                 |
| :---------------------- | :----------------------------------------------------------------------------- |
| **128-line 3D LiDAR**   | Ouster OS0-128: Horizontal: 360°, Vertical: 90° (+45° to -45°), Resolution: 1024*10Hz |
| **RGB/Stereo Camera**   | Realsense D435i: RGB: 1280*720, Stereo: 848*480, 30Hz                        |
| **Event Camera**        | Inivation Davis 346: 346*260                                                 |
| **IMU**                 | Microstrain 3DM-GX5-AHRS: 9-axis (accelerometer/gyroscope/magnetometer), 500Hz |
| **GNSS receivers**      | u-blox EVK-F9P: L1/L2 GPS/GLONASS/Galileo/BeiDou, 1Hz                         |
| **GNSS-RTK/INS**        | NovAtel SPAN-CPT7: Ground truth, RMSE: 5cm, 1Hz                               |

### Extrinsic and Intrinsic Parameters
[Sensor Extrinsic](Sensor_Parameters/sensors_extrinsic.txt)
[IMU parameters](Sensor_Parameters/gx5_imu_param.yaml)
[Camera Intrinsics](Sensor_Parameters/camera_Intrinsics.yaml)

### General Topics & its Message Type

| Topic                                    | ROS Topic                          | Message Type                                                                |
| :--------------------------------------- | :----------------------------------- | :------------------------------------------------------------------------ |
| **3D LiDAR point clouds**                | `/ouster/points`            | `sensor_msgs/PointCloud2`                                                         |
| **Stereo Camera Images**                 | `/camera/infra1/image_rect_raw` (left), `/camera/infra2/image_rect_raw` (right)                  | `sensor_msgs/Image`|
| **RGB Camera Images**                    | `/camera/color/image_raw`                  | `sensor_msgs/Image`                                                |
| **Event Camera Events**                  | `/dvs/events`                | `dvs_msgs/EventArray`                                                            |
| **9-axis IMU**                           | `/imu/data`                    | `sensor_msgs/Imu`                                                              |
| **GNSS Receiver**                        |                                      |                                                                           |
| &nbsp;&nbsp;&nbsp;GNSS raw measurement      | `/ublox_driver/range_meas`              | `gnss_comm/GnssMeasMsg`                                               |
| &nbsp;&nbsp;&nbsp;GPS/Galileo/Beidou Ephem  | `/ublox_driver/ephem`             | `gnss_comm/GnssEphemMsg`                                                   |
| &nbsp;&nbsp;&nbsp;GLONASS Ephem             | `/ublox_driver/glo_ephem`          | `gnss_comm/GnssGloEphemMsg`                                                |
| &nbsp;&nbsp;&nbsp;GNSS broadcast ionospheric parameters | `/ublox_driver/iono_params`    | `gnss_comm/StampedFloat64Array`                                              |
| &nbsp;&nbsp;&nbsp;GNSS timing message     | `/ublox_driver/time_pulse_info`     | `gnss_comm/GnssTimePulseInfoMsg`                                          |
| &nbsp;&nbsp;&nbsp;u-Blox solution         | `/ublox_driver/receiver_lla`              | `sensor_msgs/NavSatFix`                                             |
| **Ground Truth**                         | `/novatel/oem7/inspvax`          | `novatel_oem7_msgs/INSPVAX`                                                  |

## DataSets

The following table summarizes the characteristics of each sequence in our dataset:

| Name         | Size       | Duration | Distance | Average Velocity | Maximum Velocity |
| :----------- | :--------- | :------- | :------- | :--------------- | :--------------- |
| Cardiff-Seq1 | 101.2 GB   | 627s     | 2.28 Km  | 24.6 Km/h        | 36.3 Km/h        |
| Cardiff-Seq2 | 157.3 GB   | 982s     | 4.64 Km  | 28.0 Km/h        | 74.7 Km/h        |
| Cardiff-Seq3 | 74.2 GB    | 466s     | 1.12 Km  | 20.6 Km/h        | 35.5 Km/h        |
| Cardiff-Seq4 | 25.7 GB    | 159s     | 2.64 Km  | 62.3 Km/h        | 80.1 Km/h        |
| Cardiff-Seq5 | 47.8 GB    | 296s     | 4.07 Km  | 53.1 Km/h        | 76.1 Km/h        |

### Cardiff-Seq1

[TODO]

-[RINEX Observation(Raw Measurements) File](RINEX/cardiff1.obs)
-[RINEX Navigation(Ephemeris) File](RINEX/cardiff.nav)

<p align="center">
  <img width="720pix" src="GIF&Image/cardiff_1.png">
</p>
<p align="center">
  <img width="638pix" src="GIF&Image/cardiff1.gif">
</p>

### Cardiff-Seq2

[TODO]

-[RINEX Observation(Raw Measurements) File](RINEX/cardiff2.obs)
-[RINEX Navigation(Ephemeris) File](RINEX/cardiff.nav)
<p align="center">
  <img width="720pix" src="GIF&Image/cardiff_2.png">
</p>
<p align="center">
  <img width="638pix" src="GIF&Image/cardiff2.gif">
</p>

### Cardiff-Seq3

[TODO]

-[RINEX Observation(Raw Measurements) File](RINEX/cardiff3.obs)
-[RINEX Navigation(Ephemeris) File](RINEX/cardiff.nav)
<p align="center">
  <img width="720pix" src="GIF&Image/cardiff_3.png">
</p>
<p align="center">
  <img width="638pix" src="GIF&Image/cardiff3.gif">
</p>

### Cardiff-Seq4

[TODO]

-[RINEX Observation(Raw Measurements) File](RINEX/cardiff4.obs)
-[RINEX Navigation(Ephemeris) File](RINEX/cardiff.nav)
<p align="center">
  <img width="720pix" src="GIF&Image/cardiff_4.png">
</p>
<p align="center">
  <img width="638pix" src="GIF&Image/cardiff4.gif">
</p>

### Cardiff-Seq5

[TODO]

-[RINEX Observation(Raw Measurements) File](RINEX/cardiff5.obs)
-[RINEX Navigation(Ephemeris) File](RINEX/cardiff.nav)
<p align="center">
  <img width="720pix" src="GIF&Image/cardiff_5.png">
</p>
<p align="center">
  <img width="638pix" src="GIF&Image/cardiff5.gif">
</p>

## How to Use (SLAM Configuration)

### Visual Inertial Odometry

#### [VINS-Mono](config/VINS/Mono)

1.  Copy `cardiff_mono_pinhole.yaml` and `cardiff_mono_imu_config.yaml` to the `config/euroc` folder within your [VINS-Fusion](https://github.com/HKUST-Aerial-Robotics/VINS-Fusion) project directory.
2.  Launch the nodes in separate terminals:

    ```bash
    roslaunch vins vins_rviz.launch
    ```

    ```bash
    rosrun vins vins_node src/VINS-Fusion/config/euroc/cardiff_mono_imu_config.yaml
    ```

3.  Play the rosbag file:

    ```bash
    rosbag play Cardiffxxx.bag
    ```

#### [VINS-Fusion](config/VINS/Stereo)

1.  Similarly, copy `cardiff_stereo0_pinhole.yaml`, `cardiff_stereo1_pinhole.yaml`, and `cardiff_stereo_imu_config.yaml` to the `config/euroc` folder within your [VINS-Fusion](https://github.com/HKUST-Aerial-Robotics/VINS-Fusion) project directory.
2.  Launch the nodes in separate terminals:

    ```bash
    roslaunch vins vins_rviz.launch
    ```

    ```bash
    rosrun vins vins_node src/VINS-Fusion/config/euroc/cardiff_stereo_imu_config.yaml
    ```

3.  Play the rosbag file:

    ```bash
    rosbag play Cardiffxxx.bag
    ```

### LiDAR Inertial Odometry

#### [LIO-SAM](config/LIO)

1.  Copy `run_cardiff.launch` to the `launch` folder and `cardiff.yaml` to the `config` folder within your [LIO-SAM](https://github.com/TixiaoShan/LIO-SAM) project directory.
2.  Run the launch file:

    ```bash
    roslaunch lio_sam run_cardiff.launch
    ```

3.  Play the rosbag file in another terminal:

    ```bash
    rosbag play Cardiffxxx.bag
    ```