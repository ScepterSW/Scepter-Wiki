# 6. API 介绍<!-- {docsify-ignore-all} -->

## 6.1. VZ_Initialize

**函数原型：**

```cpp
VzReturnStatus VZ_Initialize()
```

**函数功能：**

完成 SDK 初始化，需要在调用其他 API 之前先调用

**函数参数：**

无

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.2. VZ_Shutdown

**函数原型：**

```cpp
VzReturnStatus VZ_Shutdown()
```

**函数功能：**

完成 SDK 注销，释放 SDK 使用过程中创建的所有资源。该接口调用之后，不应调用除 VZ_Initialize 之外的其他接口

**函数参数：**

无

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.3. VZ_GetSDKVersion

**函数原型：**

```cpp
const char* VZ_GetSDKVersion()
```

**函数功能：**

获取 SDK 的版本号：x.x.x

**函数参数：**

无

**返回值：**

- SDK 版本号

## 6.4. VZ_GetDeviceCount

**函数原型：**

```cpp
VzReturnStatus VZ_GetDeviceCount(uint32_t* pDeviceCount)
```

**函数功能：**

获取已连接的设备数目

**函数参数：**

uint32_t\* pDeviceCount：返回已连接的设备数目

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.5. VZ_GetDeviceInfo

**函数原型：**

```cpp
VzReturnStatus VZ_GetDeviceInfo(uint32_t deviceIndex, VzDeviceInfo*pDevicesInfo)
```

**函数功能：**

获取指定索引号的设备信息

**函数参数：**

uint32_t deviceIndex：设备索引号

VzDeviceInfo\* pDevicesInfo：返回设备信息

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.6. GetDeviceInfoList

**函数原型：**

```cpp
VzReturnStatus VZ_GetDeviceInfoList(uint32_t deviceCount, VzDeviceInfo* pDevicesInfoList)
```

**函数功能：**

获取 deviceCount 个数的设备信息列表

**函数参数：**

uint32_t deviceCount：需要获取信息列表的设备个数

VzDeviceInfo* pDevicesInfo：返回设备信息列表，其应该指向大小为 sizeof(VzDeviceInfo)*deviceCount 大小的缓存

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.7. VZ_OpenDeviceByUri

**函数原型：**

```cpp
VzReturnStatus VZ_OpenDeviceByUri(const char* pURI, VzDeviceHandle* pDevice)
```

**函数功能：**

使用设备标识符打开设备

**函数参数：**

const char\* pURI：设备标识符

VzDeviceHandle\* pDevice： 打开设备成功后，返回的设备句柄

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.8. VZ_OpenDeviceByAlias

**函数原型：**

```cpp
VzReturnStatus VZ_OpenDeviceByAlias(const char* pAlias, VzDeviceHandle* pDevice)
```

**函数功能：**

使用设备别名打开设备

**函数参数：**

const char\* pAlias：设备别名

VzDeviceHandle\* pDevice： 打开设备成功后，返回的设备句柄

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.9. VZ_OpenDeviceByIP

**函数原型：**

```cpp
VzReturnStatus VZ_OpenDeviceByIP(const char* pIP, VzDeviceHandle* pDevice)
```

**函数功能：**

使用设备 IP 地址打开设备

**函数参数：**

const char\* pIP：设备的 IP 地址

VzDeviceHandle\* pDevice： 打开设备成功后，返回的设备句柄

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.10. VZ_CloseDevice

**函数原型：**

```cpp
VzReturnStatus VZ_CloseDevice(VzDeviceHandle* pDevice)
```

**函数功能：**

关闭设备

**函数参数：**

VzDeviceHandle\* pDevice： 要关闭设备的句柄

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.11. VZ_StartStream

**函数原型：**

```cpp
VzReturnStatus VZ_StartStream(VzDeviceHandle device)
```

**函数功能：**

打开数据流

**函数参数：**

VzDeviceHandle device： 要关闭数据流的设备的句柄

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.12. VZ_StopStream

**函数原型：**

```cpp
VzReturnStatus VZ_StopStream(VzDeviceHandle device)
```

**函数功能：**

关闭数据流

**函数参数：**

VzDeviceHandle device： 要关闭数据流的设备的句柄

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.13. VZ_GetFrameReady

**函数原型：**

```cpp
VzReturnStatus VZ_GetFrameReady(VzDeviceHandle device, uint16_t waitTime, VzFrameReady* pFrameReady)
```

**函数功能：**

获取图像就绪状态。调用函数 VZ_GetFrame 前必须调用此函数，否则无法获取图像。

**函数参数：**

VzDeviceHandle device： 设备句柄

uint16_t waitTime：允许等待图像就绪的超时时间(ms)。此值与图像的帧率有关，建议值设置为 2\*1000/fps。例如当前的帧率为 20，则建议设置 waitTime 为 2 \* 1000 / 20 = 100。如果设置 waitTime 为 40，则调用函数时可能返回 VzRetGetFrameReadyTimeOut。

VzFrameReady\* pFrameReady：返回图像的就绪状态

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.14. VZ_GetFrame

**函数原型：**

```cpp
VzReturnStatus VZ_GetFrame(VzDeviceHandle device, VzFrameType frameType, VzFrame* pVzFrame)
```

**函数功能：**

获取指定图像类型的图像数据。调用此函数前必须调用 VZ_GetFrameReady。

**函数参数：**

VzDeviceHandle device： 设备句柄

VzFrameType frameType：待获取图像的类型

VzFrame\* pVzFrame：返回的图像数据

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.15. VZ_SetWorkMode

**函数原型：**

```cpp
VzReturnStatus VZ_SetWorkMode(VzDeviceHandle device, VzWorkMode mode)
```

**函数功能：**

设置相机的工作模式

**函数参数：**

VzDeviceHandle device： 设备句柄

VzWorkMode mode：要设置的工作模式

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.16. VZ_GetWorkMode

**函数原型：**

```cpp
VzReturnStatus VZ_GetWorkMode(VzDeviceHandle device, VzWorkMode* pMode)
```

**函数功能：**

获取相机的工作模式

**函数参数：**

VzDeviceHandle device： 设备句柄

VzWorkMode\* pMode：获取到的设备的工作模式

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.17. VZ_SetSoftwareSlaveTrigger

**函数原型：**

```cpp
VzReturnStatus VZ_SetSoftwareSlaveTrigger(VzDeviceHandle device)
```

**函数功能：**

执行一次软件触发，仅当相机处于 VzSoftwareTriggerMode 时有效

**函数参数：**

VzDeviceHandle device： 设备句柄

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.18. VZ_GetSensorIntrinsicParameters

**函数原型：**

```cpp
VzReturnStatus VZ_GetSensorIntrinsicParameters(VzDeviceHandle device, VzSensorType sensorType, VzSensorIntrinsicParameters* pSensorIntrinsicParameters)
```

**函数功能：**

获取传感器镜头的内参

**函数参数：**

VzDeviceHandle device： 设备句柄

VzSensorType sensorType：传感器类型

VzSensorIntrinsicParameters\* pSensorIntrinsicParameters：返回传感器镜头的内参

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.19. VZ_GetSensorExtrinsicParameters

**函数原型：**

```cpp
VzReturnStatus VZ_GetSensorExtrinsicParameters(VzDeviceHandle device, VzSensorExtrinsicParameters* pSensorExtrinsicParameters)
```

**函数功能：**

获取设备的外参

**函数参数：**

VzDeviceHandle device： 设备句柄

VzSensorExtrinsicParameters\* pSensorExtrinsicParameters：返回设备的外参

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.20. VZ_GetFirmwareVersion

**函数原型：**

```cpp
VzReturnStatus VZ_GetFirmwareVersion(VzDeviceHandle device, char* pFirmwareVersion, int length)
```

**函数功能：**

获取设备的固件版本

**函数参数：**

VzDeviceHandle device： 设备句柄

char\* pFirmwareVersion：返回设备的固件版本

int length：pFirmwareVersion 指向的缓存的字节长度

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.21. VZ_GetDeviceMACAddress

**函数原型：**

```cpp
VzReturnStatus VZ_GetDeviceMACAddress(VzDeviceHandle device, char* pMACAddress)
```

**函数功能：**

获取设备的 MAC 地址

**函数参数：**

VzDeviceHandle device： 设备句柄

char\* pMACAddress：返回设备的 MAC 地址，其默认是一个字节长度为 18，以‘\0’结尾的字符串

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.22. VZ_SetIRGMMGain

**函数原型：**

```cpp
VzReturnStatus VZ_SetIRGMMGain(VzDeviceHandle device, uint8_t gmmgain)
```

**函数功能：**

设置 IR 图像的数字增益

**函数参数：**

VzDeviceHandle device： 设备句柄

uint8_t gmmgain：要设置给设备的 IR 增益值

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.23. VZ_GetIRGMMGain

**函数原型：**

```cpp
VzReturnStatus VZ_GetIRGMMGain(VzDeviceHandle device, uint8_t* pGmmgain)
```

**函数功能：**

获取 IR 图像的数字增益

**函数参数：**

VzDeviceHandle device： 设备句柄

uint8_t\* pGmmgain：返回设备的 IR 增益值

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.24. VZ_SetColorPixelFormat

**函数原型：**

```cpp
VzReturnStatus VZ_SetColorPixelFormat(VzDeviceHandle device,VzPixelFormat pixelFormat)
```

**函数功能：**

设置彩色图像的像素格式

**函数参数：**

VzDeviceHandle device： 设备句柄

VzPixelFormat pixelFormat：要设置的彩色图像的像素格式

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.25. VZ_SetColorResolution

**函数原型：**

```cpp
VzReturnStatus VZ_SetColorResolution(VzDeviceHandle device, int w, int h)
```

**函数功能：**

设置彩色图像的分辨率

**函数参数：**

VzDeviceHandle device： 设备句柄

int w：图像的宽

int h：图像的高

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.26. VZ_GetColorResolution

**函数原型：**

```cpp
VzReturnStatus VZ_GetColorResolution(VzDeviceHandle device, int* pW, int* pH)
```

**函数功能：**

获取彩色图像的分辨率

**函数参数：**

VzDeviceHandle device： 设备句柄

int\* pW：返回彩色图像的图像宽

int\* pH：返回彩色图像的图像高

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.27. VZ_SetFrameRate

**函数原型：**

```cpp
VzReturnStatus VZ_SetFrameRate(VzDeviceHandle device, int value)
```

**函数功能：**

设置设备的图像帧率，同时对深度和彩色图像生效。此接口是同步接口，耗时较长，大约需要 500ms

**函数参数：**

VzDeviceHandle device： 设备句柄

int value：要设置的目标帧率

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.28. VZ_GetFrameRate

**函数原型：**

```cpp
VzReturnStatus VZ_GetFrameRate(VzDeviceHandle device, int* pValue)
```

**函数功能：**

获取设备的图像帧率

**函数参数：**

VzDeviceHandle device： 设备句柄

int\* pValue：返回设备的图像帧率

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.29. VZ_SetExposureControlMode

**函数原型：**

```cpp
VzReturnStatus VZ_SetExposureControlMode(VzDeviceHandle device, VzSensorType sensorType, VzExposureControlMode controlMode)
```

**函数功能：**

设置传感器的曝光模式

**函数参数：**

VzDeviceHandle device： 设备句柄

VzSensorType sensorType：要设置曝光模式的传感器类型

VzExposureControlMode controlMode：要设置的曝光模式

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.30. VZ_GetExposureControlMode

**函数原型：**

```cpp
VzReturnStatus VZ_GetExposureControlMode(VzDeviceHandle device, VzSensorType sensorType, VzExposureControlMode* pControlMode)
```

**函数功能：**

获取传感器的曝光模式

**函数参数：**

VzDeviceHandle device： 设备句柄

VzSensorType sensorType：要获取曝光模式的传感器类型

VzExposureControlMode controlMode：返回传感器的曝光模式

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.31. VZ_SetExposureTime

**函数原型：**

```cpp
VzReturnStatus VZ_SetExposureTime(VzDeviceHandle device, VzSensorType sensorType, VzExposureTimeParams exposureTime)
```

**函数功能：**

设置传感器的曝光时间

深度传感器，只支持在手动曝光模式下，设置曝光时间

彩色传感器，支持在自动曝光模式下，设置最大曝光时间；支持在手动曝光模式下，设置曝光时间

**函数参数：**

VzDeviceHandle device： 设备句柄

VzSensorType sensorType：要获取曝光时间的传感器类型

VzExposureTimeParams exposureTime：要设置的曝光时间参数

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.32. VZ_GetExposureTime

**函数原型：**

```cpp
VzReturnStatus VZ_GetExposureTime(VzDeviceHandle device, VzSensorType sensorType, VzExposureTimeParams* pExposureTime)
```

**函数功能：**

获取传感器的曝光时间

深度传感器，支持在手动曝光模式下，获取曝光时间；支持获取最大曝光时间

彩色传感器，支持在手动曝光模式下，获取曝光时间；支持获取最大曝光时间

**函数参数：**

VzDeviceHandle device： 设备句柄

VzSensorType sensorType：要获取曝光时间的传感器类型

VzExposureTimeParams\* pExposureTime：返回获取的曝光时间参数

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.33. VZ_SetTimeFilterEnabled

**函数原型：**

```cpp
VzReturnStatus VZ_SetTimeFilterEnabled(VzDeviceHandle device, bool bEnabled)
```

**函数功能：**

设置深度图像的时域滤波开关

**函数参数：**

VzDeviceHandle device： 设备句柄

bool bEnabled：true 表示滤波打开，false 表示滤波关闭

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.34. VZ_GetTimeFilterEnabled

**函数原型：**

```cpp
VzReturnStatus VZ_GetTimeFilterEnabled(VzDeviceHandle device, bool *pEnabled)
```

**函数功能：**

获取深度图像的时域滤波开关状态

**函数参数：**

VzDeviceHandle device： 设备句柄

bool \*pEnabled：返回滤波开关状态

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.35. VZ_SetConfidenceFilterParams

**函数原型：**

```cpp
VzReturnStatus VZ_SetConfidenceFilterParams(VzDeviceHandle device,VzConfidenceFilterParams params)
```

**函数功能：**

设置深度图像的置信度滤波参数

**函数参数：**

VzDeviceHandle device： 设备句柄

bool \*pEnabled：返回滤波开关状态

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.36. VZ_GetConfidenceFilterParams

**函数原型：**

```cpp
VzReturnStatus VZ_GetConfidenceFilterParams(VzDeviceHandle device, VzConfidenceFilterParams *pParams)
```

**函数功能：**

获取深度图像的置信度滤波参数

**函数参数：**

VzDeviceHandle device： 设备句柄

bool \*pEnabled：返回滤波开关状态

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.37. VZ_SetFlyingPixelFilterParam

**函数原型：**

```cpp
VzReturnStatus VZ_SetFlyingPixelFilterParams(VzDeviceHandle device, const VzFlyingPixelFilterParams params)
```

**函数功能：**

设置深度图像的去飞点滤波参数

**函数参数：**

VzDeviceHandle device： 设备句柄

const VzFlyingPixelFilterParams params：滤波参数

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.38. VZ_GetFlyingPixelFilterParams

**函数原型：**

```cpp
VzReturnStatus VZ_GetFlyingPixelFilterParams(VzDeviceHandle device, VzFlyingPixelFilterParams* params)
```

**函数功能：**

获取深度图像的去飞点滤波参数

**函数参数：**

VzDeviceHandle device： 设备句柄

VzFlyingPixelFilterParams\* params：滤波参数

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.39. VZ_SetFillHoleFilterParam

**函数原型：**

```cpp
VzReturnStatus VZ_SetFillHoleFilterParams(VzDeviceHandle device, const VzFillHoleFilterParams params)
```

**函数功能：**

设置深度图像的补洞滤波参数

**函数参数：**

VzDeviceHandle device： 设备句柄

const VzFillHoleFilterParams params：滤波参数

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.40. VZ_GetFillHoleFilterParams

**函数原型：**

```cpp
VzReturnStatus VZ_GetFillHoleFilterParams(VzDeviceHandle device, VzFillHoleFilterParams* params)
```

**函数功能：**

获取深度图像的补洞滤波参数

**函数参数：**

VzDeviceHandle device： 设备句柄

VzFillHoleFilterParams\* params：获取的滤波参数

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.41. VZ_SetSpatialFilterParams

**函数原型：**

```cpp
VzReturnStatus VZ_SetSpatialFilterParams(VzDeviceHandle device, const VzSpatialFilterParams params)
```

**函数功能：**

设置深度图像的空间滤波参数

**函数参数：**

VzDeviceHandle device： 设备句柄

const VzSpatialFilterParams params：滤波参数

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.42. VZ_GetSpatialFilterParams

**函数原型：**

```cpp
VzReturnStatus VZ_GetSpatialFilterParams(VzDeviceHandle device, VzSpatialFilterParams* params)
```

**函数功能：**

设置深度图像的空间滤波参数

**函数参数：**

VzDeviceHandle device： 设备句柄

VzSpatialFilterParams\* params：获取的滤波参数

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.43. VZ_SetTransformColorImgToDepthSensorEnabled

**函数原型：**

```cpp
VzReturnStatus VZ_SetTransformColorImgToDepthSensorEnabled(VzDeviceHandle device, bool bEnabled)
```

**函数功能：**

设置彩色图像对齐到深度相机空间的开关，只有带彩色传感器的设备才支持此操作。如果打开开关，则调用 VZ_GetFrameReady 时，VzFrameReady.transformedColor 的值为 1，然后调用 VZ_GetFrame 可以得到 VzTransformColorImgToDepthSensorFrame 类型的彩色图像，其大小与深度图像大小相同。

**函数参数：**

VzDeviceHandle device：设备句柄

bool bEnabled：true 打开对齐，false 关闭对齐

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.44. VZ_GetTransformColorImgToDepthSensorEnabled

**函数原型：**

```cpp
VzReturnStatus VZ_GetTransformColorImgToDepthSensorEnabled(VzDeviceHandle device, bool *bEnabled)
```

**函数功能：**

获取彩色图像对齐到深度相机空间的开关状态

**函数参数：**

VzDeviceHandle device： 设备句柄

bool \*bEnabled：返回开关状态

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.45. VZ_SetTransformDepthImgToColorSensorEnabled

**函数原型：**

```cpp
VzReturnStatus VZ_SetTransformDepthImgToColorSensorEnabled(VzDeviceHandle device, bool bEnabled)
```

**函数功能：**

设置深度图像对齐到彩色相机空间的开关，只有带彩色传感器的设备才支持此操作。如果打开开关，则调用 VZ_GetFrameReady 时，VzFrameReady.transformedDepth 的值为 1，然后调用 VZ_GetFrame 可以得到 VzTransformDepthImgToColorSensorFrame 类型的深度图像，其大小与彩色图像大小相同。

**函数参数：**

VzDeviceHandle device： 设备句柄

bool bEnabled：true 打开对齐，false 关闭对齐

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.46. VZ_GetTransformDepthImgToColorSensorEnabled

**函数原型：**

```cpp
VzReturnStatus VZ_GetTransformDepthImgToColorSensorEnabled(VzDeviceHandle device, bool *bEnabled)
```

**函数功能：**

获取深度图像对齐到彩色相机空间的开关状态

**函数参数：**

VzDeviceHandle device： 设备句柄

bool \*bEnabled：返回开关状态

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.47. VZ_TransformedDepthPointToColorPoint

**函数原型：**

```cpp
VzReturnStatus VZ_TransformedDepthPointToColorPoint(const VzDeviceHandle device, const VzDepthVector3 depthPoint, const VzVector2u16 colorSize, VzVector2u16* pPointInColor)
```

**函数功能：**

对齐深度图像上的点到彩色图像空间，可以在彩色图像上获得与传入的深度图像坐标点相对应的点的坐标

**函数参数：**

VzDeviceHandle device： 设备句柄

const VzDepthVector3 depthPoint：深度图像的坐标点

const VzVector2u16 colorSize：彩色图像尺寸

VzVector2u16\* pPointInColor：获得的与深度图像的坐标点对应的彩色图像坐标点

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.48. VZ_ConvertDepthToPointCloud

**函数原型：**

```cpp
VzReturnStatus VZ_ConvertDepthToPointCloud(VzDeviceHandle device, VzDepthVector3* pDepthVector, VzVector3f* pWorldVector, int32_t pointCount, VzSensorIntrinsicParameters* pSensorParam)
```

**函数功能：**

把传入的深度图像坐标点集合转换为世界坐标系点集合。世界坐标原点在深度传感器镜头中心，Z 轴垂直与设备前盖板，其正方向从设备指向远方；X 轴从深度镜头指向激光器，其正方向从设备指向远方；Y 轴垂直与设备指向地面，其正方向从设备指向远方。

**函数参数：**

VzDeviceHandle device： 设备句柄

VzDepthVector3\* pDepthVector：深度图像的坐标点的集合

VzVector3f\* pWorldVector：转换后点云的坐标点的集合

int32_t pointCount：坐标点的数目

VzSensorIntrinsicParameters\* pSensorParam：传感器内参

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.49. VZ_ConvertDepthFrameToPointCloudVector

**函数原型：**

```cpp
VzReturnStatus VZ_ConvertDepthFrameToPointCloudVector(VzDeviceHandle device, const VzFrame* pDepthFrame, VzVector3f* pWorldVector)
```

**函数功能：**

把传入的深度图像转换为世界坐标系点集合，转换后的世界坐标系点集合的大小为 VzFrame.width \* VzFrame.height，支持 VzDepthFrame 和 VzTransformDepthImgToColorSensorFrame 图像

**函数参数：**

VzDeviceHandle device： 设备句柄

const VzFrame\* pDepthFrame：深度图像

VzVector3f\* pWorldVector：转换后点云的坐标点的集合

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败

## 6.50. VZ_SetHotPlugStatusCallback

**函数原型：**

```cpp
VzReturnStatus VZ_SetHotPlugStatusCallback(PtrHotPlugStatusCallback pCallback, const void* pUserData)
```

**函数功能：**

设置设备热拔插状态回调函数

**函数参数：**

PtrHotPlugStatusCallback pCallback： 回调函数

const void\* pUserData：用户数据，可以为空

**返回值：**

- VzRetOK：调用成功
- 其他值：调用失败
