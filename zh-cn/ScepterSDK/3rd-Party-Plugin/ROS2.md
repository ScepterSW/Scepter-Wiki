# 4.2. ROS2

该 ROS2 软件包可用于 ScepterSDK 的深度、IR 和 Color 数据的采集和处理。

## 4.2.1. 环境要求

**1. 为您的操作系统安装推荐的 ROS2 发行版(<http://wiki.ros.org/Distributions>)**

- ROS2 安装页面：<http://docs.ros.org/en/rolling/Installation.html>

- 您可以使用第三方插件 FishROS，实现快速安装 ROS：<https://github.com/fishros/install>

**2. 已验证的版本**

| 系统         | 详情             |
| ------------ | ---------------- |
| Ubuntu 24.04 | Jazzy Jalisco    |
| Ubuntu 22.04 | Humble Hawksbill |
| Ubuntu 20.04 | Foxy Fitzroy     |

**3. 安装需要的工具**

- 安装 python 

  ```shell
  > sudo apt install python3
  ```

- 安装 colcon

  ```shell
  > sudo apt install python3-colcon-common-extensions
  ```

- 安装 pcl，仅**Jazzy Jalisco**需要

  ```shell
  > sudo apt install libpcl-dev
  ```


## 4.2.2. 安装 ROS 软件包

在 ScepterSDK 中，ScepterROS 可以用于连接单个设备，而 ScepterROS_MultiCameras 则适用于连接多个设备。

**1. 下载 Scepter ROS 包**

```shell
> git clone https://github.com/ScepterSW/ScepterSDK
```

  <div class="center">

![step0](ROS2-asserts/01.png)

  </div>

**2. 安装 Scepter ROS SDK**

```shell
> cd ROS2/src/ScepterROS
```

<div class="center">

![step2](ROS2-asserts/02.png)

</div>

通过命令"**python install.py [您的操作系统]**"，可以将与您操作系统匹配的**ScepterSDK**拷贝到**dependencies**文件夹中，这里我们以**Ubuntu20.04**为例：

```shell
> python install.py Ubuntu20.04
/home/vzense/work/ScepterSDK-master/BaseSDK
/home/vzense/work/ScepterSDK-master/3rd-PartyPlugin/ROS2/src/ScepterROS
pull SDK success
```

<div class="center">
</div>

**3. 构建 ScepterROS2 包**

<!-- tabs:start -->

#### **ROS**

```shell
> cd ../../
> colcon build --packages-select ScepterROS
```

<div class="center">

![step4](ROS2-asserts/04.png)

</div>

#### **ROS_MultiCameras**

```shell
> cd ../../
> colcon build --packages-select ScepterROS_MultiCameras
```

<div class="center">

![step6](ROS2-asserts/05.png)

</div>

<!-- tabs:end -->

```shell
> source install/setup.bash
```

## 4.2.3. 使用方式

<!-- tabs:start -->

#### **ROS**

**1. 启动相机节点**

```shell
> ros2 run ScepterROS scepter_camera
```

<div class="center">

![step6](ROS2-asserts/06.png)

</div>

**2. 启动 Rviz 界面**

```shell
> ros2 run rviz2 rviz2
```

<div class="center">

![step7](ROS2-asserts/07.png)

</div>

<div class="center">

![step8](ROS2-asserts/08.png)

</div>

**3. 使用 Rviz 显示点云**

<div class="center">

![step10](ROS2-asserts/09.png)

</div>

<div class="center">

![step11](ROS2-asserts/10.png)

</div>

#### **ROS_MultiCameras**

**1. 启动相机节点**

```shell
> ros2 run ScepterROS_MultiCameras scepter_multicameras <nodename> <ip>
```

例如：

```shell
> ros2 run ScepterROS_MultiCameras scepter_multicameras cam1 192.168.1.102
```

<div class="center">

![step6](ROS2-asserts/11.png)

</div>

**2. 启动 Rviz 界面**

一次只能显示一个话题

```shell
> ros2 run rviz2 rviz2
```

<div class="center">

![step7](ROS2-asserts/12.png)

</div>

<div class="center">

![step8](ROS2-asserts/13.png)

</div>

**3. 使用 Rviz 显示点云**

一次只能显示一个话题

<div class="center">

![step10](ROS2-asserts/14.png)

</div>

<div class="center">

![step11](ROS2-asserts/15.png)

</div>

<!-- tabs:end -->

## 4.2.4. 发布的话题

<!-- tabs:start -->

#### **ROS**

Scepter_manager 发布由 [sensor_msgs](http://wiki.ros2.org/sensor_msgs) 包定义的以下话题

- /Scepter/color/camera_info
- /Scepter/color/image_raw
- /Scepter/depth/camera_info
- /Scepter/depth/image_raw
- /Scepter/depth/points
- /Scepter/depth/points/camera_info
- /Scepter/depth2color/points
- /Scepter/depth2color/points/camera_info
- /Scepter/ir/camera_info
- /Scepter/ir/image_raw
- /Scepter/transformedColor/camera_info
- /Scepter/transformedColor/image_raw
- /Scepter/transformedDepth/camera_info
- /Scepter/transformedDepth/image_raw

#### **ROS_MultiCameras**

Scepter_manager 发布由 [sensor_msgs](http://wiki.ros2.org/sensor_msgs) 包定义的以下话题

- /**nodename**/color/camera_info
- /**nodename**/color/image_raw
- /**nodename**/depth/camera_info
- /**nodename**/depth/image_raw
- /**nodename**/depth/points
- /**nodename**/depth/points/camera_info
- /**nodename**/depth2color/points
- /**nodename**/depth2color/points/camera_info
- /**nodename**/ir/camera_info
- /**nodename**/ir/image_raw
- /**nodename**/transformedColor/camera_info
- /**nodename**/transformedColor/image_raw
- /**nodename**/transformedDepth/camera_info
- /**nodename**/transformedDepth/image_raw

<div class="center">

![topic](ROS2-asserts/16.png)

</div>

<!-- tabs:end -->

> **说明:**
>
> 1. depth2color/points 和 depth2color/points/camera_info 默认不使能，可通过如下命令打开
> ```shell
> > ros2 param set /<nodename> Depth2ColorCloudPointFlag  true
> ```
> 2. depth/points 和 depth/points/camera_info 默认使能，可通过如下命令关闭
> ```shell
> >  ros2 param set /<nodename> DepthCloudPointFlag false
> ```
> 

## 4.2.5. 编程指南

如果开发者需要设置相机参数或算法开关，请参考以下流程。
以调用**scSetSpatialFilterEnabled**为例：

- 从 **/src/ScepterROS/dependencies/include/Scepter_api.h** 查找 api

<div class="center">

![step13](ROS2-asserts/17.png)

</div>

- 将代码添加到 **/src/ScepterROS/src/scepter_manager.cpp**

<div class="center">

![step14](ROS2-asserts/18.png)

</div>

<style>
.center
{
  width: auto;
  display: table;
  margin-left: auto;
  margin-right: auto;
}
</style>
