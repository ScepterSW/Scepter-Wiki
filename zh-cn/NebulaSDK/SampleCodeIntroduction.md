# 7. 例程介绍

本篇将为您介绍如何使用 SDK 的单个 API 接口。为了帮助用户快速掌握，我们将根据产品类型进行分类，例如 DS86 & DS87、DS77、DS77C 等。这些例程涵盖了打开图像数据流、图像获取、软/硬触发、点云转换与保存等 API 接口的使用。接下来，我们将详细介绍每个例程的功能。

## 7.1. DevHotPlugCallbackC

**例程功能**

C 设置设备热插拔回调

**输出结果**

```
Get device count: 0
Get device count: 0
Get device count: 1
uri:***
alias:***
ip:192.168.1.101
connectStatus:2
open device successful,status :0
 wait for hotplug operation
uri 1  ***    remove
alias 1  ***    remove
VZ_StopStream 0
VZ_CloseDevice 0
uri 0  ***    add
alias 0  ***    add
VZ_OpenDevice 0
VZ_StartStream 0
```

## 7.2. DevHotPlugCallbackCpp

**例程功能**

C++设置设备热插拔回调

**输出结果**

```
Get device count: 0
Get device count: 0
Get device count: 1
uri:***
alias:***
ip:192.168.1.101
connectStatus:2
open device successful,status :0
 wait for hotplug operation
uri 1  ***    remove
alias 1  ***    remove
VZ_StopStream 0
VZ_CloseDevice 0
uri 0  ***    add
alias 0  ***    add
VZ_OpenDevice 0
VZ_StartStream 0
```

## 7.3. DeviceConnectByAlias

**例程功能**

设置设备通过设备 SN 连接

**输出结果**

```
Get device count: 0
Get device count: 0
Get device count: 1
uri:***
alias:***
ip:192.168.1.101
connectStatus:2
```

## 7.4. DeviceConnectByIP

**例程功能**

设置设备通过 IP 地址链接

**输出结果**

```
Get device count: 0
Get device count: 0
Get device count: 1
uri:***
alias:***
ip:192.168.1.101
connectStatus:2
```

## 7.5. DeviceHWTriggerMode

**例程功能**

设置设备为硬触发模式

**输出结果**

```
Get device count: 0
Get device count: 0
Get device count: 1
uri:***
alias:***
ip:192.168.1.101
connectStatus:2
Hardware trigger test begins
```

## 7.6. DeviceSWTriggerMode

**例程功能**

设置设备为软触发模式

**输出结果**

```
Get device count: 0
Get device count: 0
Get device count: 1
uri:***
alias:***
ip:192.168.1.101
connectStatus:2
Software trigger test begins
```

## 7.7. DeviceInfoGet

**例程功能**

获取设备 SN、IP 地址、固件版本信息

**输出结果**

```
Get device count: 0
Get device count: 0
Get device count: 1
uri:***
alias:***
ip:192.168.1.101
connectStatus:2
FirmwareVersionNum:***
```

## 7.8. DeviceParamSetGet

**例程功能**

获取设备内外参、畸变参数，设置获取设备 GmmaGian 值

**输出结果**

```
Get device count: 0
Get device count: 0
Get device count: 1
uri:***
alias:***
ip:192.168.1.101
connectStatus:2

Get VzGetCameraParameters status: 0
Depth Camera Intinsic:
Fx: ***
Cx: ***
Fy: ***
Cy: ***
Depth Distortion Coefficient:
K1: ***
K2: ***
P1: ***
P2: ***
K3: ***
K4: ***
K5: ***
K6: ***

default gmmgain: 100
set gmmgain: 100 succeeded
```

## 7.9. DeviceSearchAndConnect

**例程功能**

搜索并连接设备

**输出结果**

```
Get device count: 0
Get device count: 0
Get device count: 1
uri:***
alias:***
connectStatus:2
open device successful,status :0
```

## 7.10. DeviceSetFrameRate

**例程功能**

设置设备帧率

**输出结果**

```
Get device count: 0
Get device count: 0
Get device count: 1
open device successful,status :0
set frame rate :5 is OK.
Start testing the average frame rate for 30 seconds, Please wait patiently
```

## 7.11. DeviceSetParamsByJson

**例程功能**

通过 Json 设置设备参数

**输出结果**

```
Get device count: 0
Get device count: 0
Get device count: 1
uri:***
alias:***
ip:192.168.1.101
connectStatus:2
Please input Json file path:
***
VZ_SetParamsByJson ret:0
```

## 7.12. DeviceStartStopStreaming

**例程功能**

开始与停止设备数据流

**输出结果**

```
Get device count: 0
Get device count: 0
Get device count: 1
uri:***
alias:***
ip:192.168.1.101
connectStatus:2
```

## 7.13. FrameCaptureAndSave

**例程功能**

捕获与保存设备图像

**输出结果**

```
Get device count: 0
Get device count: 0
Get device count: 1
uri:***
alias:***
ip:192.168.1.101
connectStatus:2
get Frame successful,status:0  Save...
```

## 7.14. MultiConnection

**例程功能**

多设备连接

**输出结果**

```
Get device count: 0
Get device count: 0
Get device count: 2
CameraIndex: 0
uri:***
alias:***
connectStatus:2
CameraIndex: 1
uri:***
alias:***
connectStatus:2
*** frameIndex :22
*** frameIndex :17
*** frameIndex :23
*** frameIndex :18
*** frameIndex :24
*** frameIndex :19
```

## 7.15. MultiConnectionInMultiThread

**例程功能**

在多线程中多设备连接

**输出结果**

```
Get device count: 0
Get device count: 0
Get device count: 2
uri:DS77Lite:***
uri:DS77Lite:***
alias:***
connectStatus:2
alias:***
connectStatus:2
*** frameIndex :8
*** frameIndex :9
*** frameIndex :10
*** frameIndex :11
*** frameIndex :12
*** frameIndex :8
*** frameIndex :9
*** frameIndex :10
*** frameIndex :11
*** frameIndex :12
```

## 7.16. PointCloudCaptureAndSave

**例程功能**

捕获与保存点云

**输出结果**

```
Get device count: 0
Get device count: 0
Get device count: 1
uri:***
alias:***
ip:192.168.1.101
connectStatus:2
Save point cloud successful in PointCloud.txt
```

## 7.17. PointCloudCaptureAndSaveDepthImgToColorSensor

**例程功能**

捕获点云并且将其保存到彩色图像传感器

**输出结果**

```
Get device count: 0
Get device count: 0
Get device count: 1
uri:***
alias:***
ip:192.168.1.101
connectStatus:2
open device successful,status :0
set to 800_600
VZ_SetTransformDepthImgToColorSensorEnabled Enabled
get Frame successful,status:0  frameTpye:5  frameIndex:12
800,600
Save point cloud successful in PointCloud.txt
```

## 7.18. PointCloudVectorAndSave

**例程功能**

捕获与保存 ROI 区域中的点云

**输出结果**

```
Get device count: 0
Get device count: 0
Get device count: 1
uri:***
alias:***
ip:192.168.1.101
connectStatus:2
open device successful,status :0
Save point cloud successful in PointCloud.txt
```

## 7.19. PointCloudVectorAndSaveDepthImgToColorSensor

**例程功能**

捕获 ROI 区域中的点云并且将其保存到彩色图像传感器

**输出结果**

```
Get device count: 0
Get device count: 0
Get device count: 1
uri:***
alias:***
ip:192.168.1.101
connectStatus:2
open device successful,status :0
set to 800_600
VZ_SetTransformDepthImgToColorSensorEnabled Enabled
get Frame successful,status:0  frameTpye:5  frameIndex:12
800,600
Save point cloud successful in PointCloud.txt
```

## 7.20. RGBExposureTimeSetGet

**例程功能**

设置获取设备 RGB 曝光时间

**输出结果**

```
Get device count: 0
Get device count: 0
Get device count: 1
uri:***
alias:***
ip:192.168.1.101
connectStatus:2
open device successful,status :0

---- To  VzExposureControlMode_Manual ----
VZ_SetExposureControlMode  ok
* step1. Get Color exposure time range with frameRate 5*
Recommended scope: 100 - 30000
* step2. Set and Get new ExposureTime *
SetExposureTime:3000
GetExposureTime:3000

---- To VzExposureControlMode_Auto ----
VZ_SetExposureControlMode ok
* step1. Get Color exposure time range *
Recommended scope: 100 - 30000
* step2. Set and Get new Auto Max Color exposure time range *
SetExposureTimeAutoMax:10000
GetExposureTimeAutoMax:10000
```

## 7.21. RGBResolutionChange

**例程功能**

更改设备 RGB 分辨率

**输出结果**

```
Get device count: 0
Get device count: 0
Get device count: 1
uri:***
alias:***
ip:192.168.1.101
connectStatus:2
open device successful,status :0
set to 640_480
get Frame successful,status:0  resolution: 640x480
get Frame successful,status:0  resolution: 640x480
get Frame successful,status:0  resolution: 640x480
get Frame successful,status:0  resolution: 640x480
get Frame successful,status:0  resolution: 640x480
get Frame successful,status:0  resolution: 640x480
get Frame successful,status:0  resolution: 640x480
get Frame successful,status:0  resolution: 640x480
get Frame successful,status:0  resolution: 640x480
get Frame successful,status:0  resolution: 640x480
set to 1600_1200
get Frame successful,status:0  resolution: 1600x1200
get Frame successful,status:0  resolution: 1600x1200
get Frame successful,status:0  resolution: 1600x1200
get Frame successful,status:0  resolution: 1600x1200
get Frame successful,status:0  resolution: 1600x1200
get Frame successful,status:0  resolution: 1600x1200
get Frame successful,status:0  resolution: 1600x1200
get Frame successful,status:0  resolution: 1600x1200
get Frame successful,status:0  resolution: 1600x1200
get Frame successful,status:0  resolution: 1600x1200
```

## 7.22. ToFExposureTimeSetGet

**例程功能**

设置获取设备 ToF 曝光时间

**输出结果**

```
---- ToFExposureTimeSetGet ----
Get device count: 0
Get device count: 0
Get device count: 1
uri:***
alias:***
ip:192.168.1.101
connectStatus:2
Open device successful,status :0

---- Default FrameRate ----
Set control mode to manual.
Get default frame rate: 30
Recommended scope: 58 - 6600
```

## 7.23. ToFFiltersSetGet

**例程功能**

设置获取设备 ToF 滤波开关

**输出结果**

```
--------------ToFFiltersSetGet-------------
Get device count: 0
Get device count: 0
Get device count: 1
uri:***
alias:***
ip:192.168.1.101
connectStatus:2
open device successful,status :0

-------------1------------ test TimeFilter --------------------------
The default TimeFilter switch is true
Set TimeFilter switch to false is Ok.

-------------2--------- test ConfidenceFilter -----------------------
The default ConfidenceFilter switch is true
Set ConfidenceFilter switch to false is Ok.

-------------3--------- test FlyingPixelFilter ----------------------
The default FlyingPixelFilter switch is true
Set FlyingPixelFilter switch to false is Ok.

-------------4---------- test FillHoleFilter ------------------------
The default FillHoleFilter switch is true
Set FillHoleFilter switch to false is Ok.

-------------5---------- test SpatialFilter -------------------------
The default SpatialFilter switch is false
Set SpatialFilter switch to true is Ok.
```

## 7.24. TransformColorImgToDepthSensorFrame

**例程功能**

将彩色图像对齐到设备的深度图像空间

**输出结果**

```
---TransformColorImgToDepthSensorFrame---
Get device count: 0
Get device count: 0
Get device count: 1
uri:***
alias:***
ip:192.168.1.101
connectStatus:2
open device successful,status :0
VZ_SetTransformColorImgToDepthSensorEnabled  Enabled
get Frame successful,status:0  frameTpye:4  frameIndex:11
get Frame successful,status:0  frameTpye:4  frameIndex:12
get Frame successful,status:0  frameTpye:4  frameIndex:13
get Frame successful,status:0  frameTpye:4  frameIndex:14
get Frame successful,status:0  frameTpye:4  frameIndex:15

```

## 7.25. TransformDepthImgToColorSensorFrame

**例程功能**

将深度图像对齐到设备的彩色图像空间

**输出结果**

```
---TransformColorImgToDepthSensorFrame---
Get device count: 0
Get device count: 0
Get device count: 1
uri:***
alias:***
ip:192.168.1.101
connectStatus:2
open device successful,status :0
VZ_SetTransformDepthImgToColorSensorEnabled  Enabled
get Frame successful,status:0  frameTpye:4  frameIndex:11
get Frame successful,status:0  frameTpye:4  frameIndex:12
get Frame successful,status:0  frameTpye:4  frameIndex:13
get Frame successful,status:0  frameTpye:4  frameIndex:14
get Frame successful,status:0  frameTpye:4  frameIndex:15
```
