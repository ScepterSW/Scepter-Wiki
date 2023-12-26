# ROS2 多相机连接

## 概述

该 ROS2 软件包可用于 NebulaSDK 的深度、IR 和 RGB 数据的采集和处理

## 安装

- **为您的操作系统安装推荐的 [ROS2 发行版](http://wiki.ros.org/Distributions)**

  - [ROS2 安装页面](http://docs.ros.org/en/rolling/Installation.html)

- **已验证的版本**
  |系统|详情|
  |---|---|
  |Ubuntu20.04|Foxy Fitzroy|
  |Ubuntu18.04|Eloquent Elusor|

- **安装 Vzense ROS2 软件包**

  - [安装 NebulaSDK](https://gitee.com/Vzense/NebulaSDK)

    ```console
    git clone https://gitee.com/Vzense/NebulaSDK
    ```

    <div class="center">

    ![step0](pic/ROS2_MultiCameras/step0.png)

    </div>

  - **将 SDK 更新为 ROS2 包**

    ```console
    cd ROS2/src/VzenseROS_MultiCameras
    ```

    <div class="center">

    ![step2](pic/ROS2_MultiCameras/step2.png)

    </div>

  - **install.py**: 通过命令"**python install.py (您的操作系统)**"，可以将与您操作系统匹配的**NebulaSDK**拷贝到**dependencies**文件夹中, 这里我们以**Ubuntu18.04**为例：

    ```console
    python install.py Ubuntu18.04
    ```

    <div class="center">

    ![step3](pic/ROS2_MultiCameras/step3.png)

    </div>

- **构建 VzenseRO2 包**

如果没有安装 colcon，请先运行 cmd：

```console
sudo apt install python3-colcon-common-extensions
```

```console
cd ../../
colcon build --packages-select VzenseROS_MultiCameras
```

<div class="center">

![step4](pic/ROS2_MultiCameras/step4.png)

</div>

- **环境设置**

```console
source install/setup.bash
```

## 使用方式

- **启动相机节点**

  ```console
  ros2 run VzenseROS_MultiCameras vzense_multicameras <nodename> <ip>
  ```

  例如：

  ```console
  ros2 run VzenseROS_MultiCameras vzense_multicameras cam1 192.168.1.102
  ```

  <div class="center">

  ![step6](pic/ROS2_MultiCameras/step6.png)

  </div>

- **Rviz**

  一次只能显示一个话题

- **启动 Rviz 界面**

  ```console
  ros2 run rviz2 rviz2
  ```

  <div class="center">

  ![step7](pic/ROS2_MultiCameras/step7.png)

  </div>

  <div class="center">

  ![step8](pic/ROS2_MultiCameras/step8.png)

  </div>

- **使用 Rviz 显示点云**

  <div class="center">

  ![step10](pic/ROS2_MultiCameras/step10.png)

  </div>

  <div class="center">

  ![step11](pic/ROS2_MultiCameras/step11.png)

  </div>

## 发布的话题

Vzense_manager 发布由 [sensor_msgs](http://wiki.ros2.org/sensor_msgs) 包定义的以下话题

- /**nodename**/color/camera_info
- /**nodename**/color/image_raw
- /**nodename**/depth/camera_info
- /**nodename**/depth/image_raw
- /**nodename**/depth/points
- /**nodename**/depth/points/camera_info
- /**nodename**/ir/camera_info
- /**nodename**/ir/image_raw
- /**nodename**/transformedColor/camera_info
- /**nodename**/transformedColor/image_raw
- /**nodename**/transformedDepth/camera_info
- /**nodename**/transformedDepth/image_raw

<div class="center">

![topic](pic/ROS2_MultiCameras/topic.png)

</div>

## 编程指南

如果开发者需要设置相机参数或算法开关，请参考以下流程。
以调用**VZ_SetSpatialFilterEnabled**为例：

- 从**dependencies/Include/VzenseNebula_api.h**查找 api

<div class="center">

![step13](pic/ROS2_MultiCameras/step13.png)

</div>

- 将代码添加到 **/src/vzense_manager.cpp**

<div class="center">

![step14](pic/ROS2_MultiCameras/step14.png)

</div>

## 说明

- 当使用多个网卡时，需要设置不同的 IP 网段。

<style>
.center
{
  width: auto;
  display: table;
  margin-left: auto;
  margin-right: auto;
}
</style>
