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

**1. 下载 Scepter ROS 包**

```shell
> git clone https://github.com/ScepterSW/ScepterSDK
```

  <div class="center">

![step0](ROS2-asserts/01.png)

  </div>

**2. 安装 Scepter ROS SDK**

```shell
> cd SDK/3rd-PartyPlugin/ROS2
```

<div class="center">

![step2](ROS2-asserts/02.png)

</div>

>./src
>
>├── sc_enumerate_devices -- 用于Vzense相机枚举，获取相机IP、Series Number与Camera Status等信息；
>
>├── scepter_manager -- 用于连接Vzense相机，进行Depth、IR 与 Color 数据的采集和处理；

通过执行命令"**python3 scepter_sdk_install.py**"，可以将Scepter ROS2 Wrapper所需的依赖项拷贝到**dependencies**文件夹中；

以**Ubuntu20.04**系统为例：

```shell
> python3 scepter_sdk_install.py
```

```shell
Dependencies of package <scepter_manager> have installed successfully on Platform Ubuntu20.04
Dependencies of package <sc_enumerate_devices> have installed successfully on Platform Ubuntu20.04
```

**3.  构建ScepterROS2包**

```shell
> cd SDK/3rd-PartyPlugin/ROS2
```
 
- 构建sc_enumerate_devices

```shell
> colcon build --packages-select sc_enumerate_devices
```

```shell
Starting >>> sc_enumerate_devices
Finished <<< sc_enumerate_devices [3.47s]
Summary: 1 packages finished [3.5s]
```

```shell
> source install/setup.bash
```

获取设备信息和状态

```shell
> ros2 run sc_enumerate_devices sc_enumerate_devices 
```

```shell
[INFO] [1751508675.828313553] [sc_enumerate_devices]: Find device successfully, The device count is : 1
[INFO] [1751508675.828385016] [sc_enumerate_devices]: device 1 ip 192.168.1.103 seriesnumber GN6501PBCA7100393 status 1
```
<div class="center">

![step6](ROS2-asserts/04.png)

</div>

更新seriesnumber到/SDK/3rd-PartyPlugin/ROS2/src/scepter_manager/param/default.param.yaml

以**GN6501PBCA7100393**为例，

```yaml
/**:
  ros__parameters:
    camera_name: "tof_camera" # camera name, node name would be set as vzense_{camear_name}.
    camera_sn: "GN6501PBCA7100393" # camera series number.
    framerate: 15 # camera frame rate.
    work_mode: 0 # camera work mode. 0: Active Mode 1: HardwareTrigger Mode 2: SoftwareTigger Mode.
    color_resolution: 0 # camera color resolution. 0: 1600*1200 1: 800*600 2: 640*480.
    xdr_mode: 0 # camera hdr&wdr mode. 0: hdr disable wdr disable 1: hdr enable wdr diable 2: hdr disable wdr enable.
    depth_publish: true # whether publish depth image.
    ir_publish: true # whether publish ir image.
    color_publish: true # whether publish color image.
    transformed_color: false # whether enable color to depth transformation and publish it.
    transformed_depth: false # whether enable depth to color transformation and publish it.
    depth_cloud_point: false # whether publish depth cloud point.
    depth2color_cloud_point: false # whether publish depth2color cloud point, must works with the transformed_depth enabled.
```

- 构建scepter_manager
 
```shell
> colcon build --packages-select scepter_manager
``` 
 
```shell
Starting >>> scepter_manager
Finished <<< scepter_manager [13.6s]                       
Summary: 1 package finished [13.7s]
``` 

<div class="center">

![step4](.\ROS2-asserts\03.png)

</div>

```shell
> source install/setup.bash
```
## 4.2.3. 使用方式
<!-- tabs:start -->

### **单设备**

**1. 启动相机节点**

```shell
> ros2 launch scepter_manager node_execute.launch.py
```

<div class="center">

![./ROS2-asserts/05.png](.\ROS2-asserts\05.png)

</div>

>设置帧率20，Color分辨率640*480，其余参数仍是yaml文件的配置
>
>```shell
> >ros2 launch scepter_manager node_execute.launch.py framerate:=20 color_resolution:=2
>```

**2. 相机动态参数设置**

查看参数列表；

```Shell
> ros2 param list /vzense_tof_camera
```

```Shell
  camera_name // 不可动态修改
  camera_sn   // 不可动态修改
  color_publish
  color_resolution
  depth2color_cloud_point
  depth_cloud_point
  depth_publish
  framerate
  ir_publish
  software_trigger
  transformed_color
  transformed_depth
  use_sim_time
  work_mode
  xdr_mode
```

<!-- tabs:start -->
### **方式1**

```shell
> ros2 param set /vzense_tof_camera depth_cloud_point true
``` 

### **方式2**

```shell
> rqt
```

<div class="center">

![](.\ROS2-asserts\09.png)

</div>

<!-- tabs:end -->

**3. Topic列表**

scepter_manager 发布由 [sensor_msgs](http://wiki.ros.org/sensor_msgs) 包定义的以下话题 

```shell
/tf_static -- Static TF info
/vzense_tof_camera/<sn>/color/camera_info -- Color sensor camera info
/vzense_tof_camera/<sn>/color/image_raw -- Color image
/vzense_tof_camera/<sn>/depth/camera_info -- Depth sensor camera info
/vzense_tof_camera/<sn>/depth/image_raw -- Depth image
/vzense_tof_camera/<sn>/depth/points -- Depth cloud point
/vzense_tof_camera/<sn>/depth/points/camera_info -- Depth sensor camera info with depth cloud point frame id
/vzense_tof_camera/<sn>/depth2color/points -- Depth-to-color cloud point
/vzense_tof_camera/<sn>/depth2color/points/camera_info -- Color sensor camera info with depth-to-color cloud point frame id
/vzense_tof_camera/<sn>/ir/camera_info -- Depth sensor camera info with IR frame id
/vzense_tof_camera/<sn>/ir/image_raw -- IR image
/vzense_tof_camera/<sn>/transformedColor/camera_info -- Depth sensor camera info with color-to-depth frame id
/vzense_tof_camera/<sn>/transformedColor/image_raw -- Color-to-depth aligned image
/vzense_tof_camera/<sn>/transformedDepth/camera_info -- Color sensor camera info with depth-to-color frame id
/vzense_tof_camera/<sn>/transformedDepth/image_raw -- Depth-to-color aligned image
```

>部分Topic默认不发布，需动态调整参数后使能

**4. 使用 Rviz2 订阅 Topic**

```shell
> ros2 run rviz2 rviz2
```

- 订阅Color图像

Color图像的Topic名称为：/color/image_raw

<div class="center">

![step7](ROS2-asserts/06.png)

</div>

<div class="center">

![step8](ROS2-asserts/07.png)

</div>

- 订阅Depth点云

Depth点云Topic名称为：/depth/points

```shell
> rqt
```

<div class="center">

![step10](ROS2-asserts/09.png)

</div>

> 默认情况下，相机启动时不会发布该Topic，可以使用rqt进行动态设置。

<div class="center">

![step11](ROS2-asserts/10.png)

![](.\ROS2-asserts\11.png)

</div>

**5. Intra Process Communication 支持**

```Shell
> ros2 launch scepter_manager node_container.launch.py
```

<div class="center">

![](.\ROS2-asserts\14.png)

</div>

### **多设备**

**1. 启动多个相机节点**

以启动两个相机为例；

设置camera1的帧率为25，且发布Depth点云；

设置camera2的帧率为14，分辨率为648 * 480；

其余参数使用/param/default.param.yaml内的默认值；

命令如下：

```shell
> ros2 launch scepter_manager node_execute_multi.launch.py camera_sn1:="GN6501PBCA7100393" camera_sn2:="GN650SCBCA3310124" framerate1:=25 framerate2:=14  depth_cloud_point1:=true color_resolution2:=2
```

<div class="center">

![](.\ROS2-asserts\12.png)

</div>

>
> - 多设备当前仅支持如上方式启动，暂不支持多个yaml文件。
> - 仅可以设置/param/default.param.yaml内的参数，输入参数命名格式**paramname\<ID\>**, 以camera_sn为例，amera_sn1:="GN6501PBCA7100393" camera_sn2:="GN650SCBCA3310124"
> - 未设置的参数，使用/param/default.param.yaml内的默认值。
>

**2. 相机动态参数设置**

使用方式同单设备，仅选择的节点名称不同。

**3. 多相机Topic列表**

scepter_manager 发布由 [sensor_msgs](http://wiki.ros.org/sensor_msgs) 包定义的以下话题 ：

```shell
/tf_static
/vzense_tof_camera1/<sn1>/color/camera_info
/vzense_tof_camera1/<sn1>/color/image_raw
/vzense_tof_camera1/<sn1>/depth/camera_info
/vzense_tof_camera1/<sn1>/depth/image_raw
/vzense_tof_camera1/<sn1>/depth/points
/vzense_tof_camera1/<sn1>/depth/points/camera_info
/vzense_tof_camera1/<sn1>/depth2color/points
/vzense_tof_camera1/<sn1>/depth2color/points/camera_info
/vzense_tof_camera1/<sn1>/ir/camera_info
/vzense_tof_camera1/<sn1>/ir/image_raw
/vzense_tof_camera1/<sn1>/transformedColor/camera_info
/vzense_tof_camera1/<sn1>/transformedColor/image_raw
/vzense_tof_camera1/<sn1>/transformedDepth/camera_info
/vzense_tof_camera1/<sn1>/transformedDepth/image_raw
/vzense_tof_camera2/<sn2>/color/camera_info
/vzense_tof_camera2/<sn2>/color/image_raw
/vzense_tof_camera2/<sn2>/depth/camera_info
/vzense_tof_camera2/<sn2>/depth/image_raw
/vzense_tof_camera2/<sn2>/depth/points
/vzense_tof_camera2/<sn2>/depth/points/camera_info
/vzense_tof_camera2/<sn2>/depth2color/points
/vzense_tof_camera2/<sn2>/depth2color/points/camera_info
/vzense_tof_camera2/<sn2>/ir/camera_info
/vzense_tof_camera2/<sn2>/ir/image_raw
/vzense_tof_camera2/<sn2>/transformedColor/camera_info
/vzense_tof_camera2/<sn2>/transformedColor/image_raw
/vzense_tof_camera2/<sn2>/transformedDepth/camera_info
/vzense_tof_camera2/<sn2>/transformedDepth/image_raw
```

**4. Rviz2订阅**

使用方式同单设备，仅示例订阅camera1的Color与Depth点云及camera2的Depth：

<div class="center">

![step6](ROS2-asserts/13.png)

</div>

**5. Intra Process Communication 支持**

```shell
> ros2 launch scepter_manager node_container_multi.launch.py camera_sn1:="GN6501PBCA7100393" camera_sn2:="GN650SCBCA3310124" framerate1:=25 framerate2:=14  depth_cloud_point1:=true color_resolution2:=2
```

<div class="center">

![](.\ROS2-asserts\15.png)

</div>
 
<!-- tabs:end -->
## 4.2.4. 编程指南

如果开发者需要设置其余相机参数或算法开关，请参考以下流程。
以调用**scSetSpatialFilterEnabled**为例：

- 从 **/src/scepter_manger/dependencies/include/Scepter_api.h** 查找 api

<div class="center">

![step13](ROS2-asserts/17.png)

</div>

- 将代码添加到 **/src/scepter_manger/src/scepter_manager.cpp**

<div class="center">

![step14](ROS2-asserts/18.png)

</div>

## 4.2.5. ROS2 Samples

**1. Samples简介**

ROS2_Samples/src目录下，提供6个package，演示订阅图像和点云：

```Shell
├── device_sw_trigger_mode -- 订阅SoftwareTigger模式下相机节点的Depth/Ir/Color图像
├── frame_capture_and_save -- 订阅Active模式下相机节点的Depth/Ir/Color图像
├── point_cloud_capture_and_save -- 订阅Active模式下相机节点的Depth点云
├── point_cloud_capture_and_save_depthimg_to_color_sensor -- 订阅Active模式下相机节点的Depth-to-Color点云
├── transform_colorimg_to_depth_sensor_frame -- 订阅Active模式下相机节点的Color-to-Depth图像
└── transform_depthimg_to_color_sensor_frame-- 订阅Active模式下相机节点的Depth-to-Color图像
```

**2. Samples编译**

```shell
> cd SDK/3rd-PartyPlugin/ROS2_Samples
> colcon build
```

```shell
Starting >>> device_sw_trigger_mode
Starting >>> frame_capture_and_save
Starting >>> point_cloud_capture_and_save
Starting >>> point_cloud_capture_and_save_depthimg_to_color_sensor
Starting >>> transform_colorimg_to_depth_sensor_frame
Starting >>> transform_depthimg_to_color_sensor_frame
Finished <<< frame_capture_and_save [17.0s]                                                    
Finished <<< transform_colorimg_to_depth_sensor_frame [17.1s]                     
Finished <<< transform_depthimg_to_color_sensor_frame [17.3s]              
Finished <<< device_sw_trigger_mode [17.7s]          
Finished <<< point_cloud_capture_and_save_depthimg_to_color_sensor [26.3s]
Finished <<< point_cloud_capture_and_save [26.9s]

Summary: 6 packages finished [27.1s]
```
**3. Samples执行**

- 获取需要连接的相机节点的名称

```shell
> ros2 node list
```

```shell
/static_tf_vzense_camera_node  --- 静态TF发布的节点
/vzense_tof_camera             --- Vzense的相机节点
```

- 运行用例，订阅指定相机节点

```shell
> ros2 run device_sw_trigger_mode device_sw_trigger_mode --ros-args -p node_name:="/vzense_tof_camera"

> ros2 run frame_capture_and_save frame_capture_and_save --ros-args -p node_name:="/vzense_tof_camera"

> ros2 run point_cloud_capture_and_save point_cloud_capture_and_save --ros-args -p node_name:="/vzense_tof_camera"

> ros2 run point_cloud_capture_and_save_depthimg_to_color_sensor point_cloud_capture_and_save_depthimg_to_color_sensor  --ros-args -p node_name:="/vzense_tof_camera"

> ros2 run transform_colorimg_to_depth_sensor_frame transform_colorimg_to_depth_sensor_frame  --ros-args -p node_name:="/vzense_tof_camera"

> ros2 run transform_depthimg_to_color_sensor_frame transform_depthimg_to_color_sensor_frame  --ros-args -p node_name:="/vzense_tof_camera"
```

>
> 用例在执行后，订阅数据存储到对应package的目录下。
>
<style>
.center
{
  width: auto;
  display: table;
  margin-left: auto;
  margin-right: auto;
}
</style>