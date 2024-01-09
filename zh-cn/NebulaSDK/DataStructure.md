# 5. 数据结构

## 5.1. Enum 数据类型

### 5.1.1. VzFrameType

**功能：**

图像类型。

_PS:不同型号产品对应的枚举值个数可能不同，请以具体型号文件夹下定义为准。_

**枚举值：**

- VzDepthFrame：表示深度图像类型
- VzIRFrame：表示灰度图像类型
- VzColorFrame：表示彩色图像类型
- VzTransformColorImgToDepthSensorFrame：表示映射到深度传感器空间的彩色图像类型
- VzTransformDepthImgToColorSensorFrame：表示映射到彩色传感器空间的深度图像类型
- VzConfidenceFrame：表示激光强度图像

### 5.1.2. VzPixelFormat

**功能：**

图像数据的像素类型。

_PS:不同型号产品对应的枚举值个数可能不同，请以具体型号文件夹下定义为准。_

**枚举值：**

- VzPixelFormatDepthMM16：表示每个像素数据为 16 位的深度值，单位为毫米
- VzPixelFormatGray8：表示每个像素数据为 8 位的灰度值
- VzPixelFormatRGB888：表示每个像素数据为 24 位的 RGB 值
- VzPixelFormatBGR888：表示每个像素数据为 24 位的 BGR 值

### 5.1.3. VzSensorType

**功能：**

传感器类型。

_PS:不同型号产品对应的枚举值个数可能不同，请以具体型号文件夹下定义为准。_

**枚举值：**

- VzToFSensor：表示深度数据传感器
- VzColorSensor：表示彩色图像传感器

### 5.1.4. VzReturnStatus

**功能：**

接口函数的返回值。

_PS:不同型号产品对应的枚举值个数可能不同，请以 Include 中具体型号文件夹下定义为准。_

**枚举值：**

- VzRetOK：表示调用成功
- VzRetNoDeviceConnected：表示当前无设备连接
- VzRetInvalidDeviceIndex：表示传入的设备序号无效
- VzRetDevicePointerIsNull：表示传入的设备指针为空
- VzRetInvalidFrameType：表示传入的图像类型无效
- VzRetFramePointerIsNull：表示传入的图像指针为空
- VzRetNoPropertyValueGet：表示无法获取当前属性值
- VzRetNoPropertyValueSet：表示无法设置当前属性值
- VzRetPropertyPointerIsNull：表示传入的指向存储属性值的缓存指针为空
- VzRetPropertySizeNotEnough：表示传入的指向存储属性值的缓存空间不足
- VzRetInvalidDepthRange：表示传入的 depth range 无效
- VzRetGetFrameReadyTimeOut：表示获取图像时超时
- VzRetInputPointerIsNull：表示传入的指针为空
- VzRetCameraNotOpened：表示相机未打开
- VzRetInvalidCameraType：表示传入的相机类型无效
- VzRetInvalidParams：表示传入的参数无效
- VzRetCurrentVersionNotSupport：表示当前版本不支持
- VzRetUpgradeImgError：表示升级相机固件失败
- VzRetUpgradeImgPathTooLong：表示传入的相机固件路径长度太长
- VzRetUpgradeCallbackNotSet：表示未设置相机升级时的回调函数
- VzRetNoAdapterConnected：表示电源适配器未连接
- VzRetReInitialized：表示重复初始化
- VzRetNoInitialized：表示未做初始化
- VzRetCameraOpened：表示相机已经打开
- VzRetCmdError：表示命令下发失败
- VzRetCmdSyncTimeOut：表示命令发送成功，但是同步匹配失败
- VzRetIPNotMatch：表示相机 IP 与主机 IP 不在同一网段
- VzRetNotStopStream：表示未打开数据流
- VzRetOthers：表示其他错误

### 5.1.5. VzConnectStatus

**功能：**

设备连接状态。

_PS:不同型号产品对应的枚举值个数可能不同，请以 Include 中具体型号文件夹下定义为准。_

**枚举值：**

- VzConnectUNKNOWN：表示连接状态未知
- VzUnconnected：表示设备未连接
- VzConnected：表示设备已连接
- VzOpened：表示设备已被打开
- VzUpgradeUnconnected：表示设备处于升级待连接状态
- VzUpgradeConnected：表示设备处于升级状态且已连接

### 5.1.6. VzDeviceType

**功能：**

设备类型。

**枚举值：**

- VzDS86：表示 DS86 相机，使用 RJ45 接口，同时提供 ToF+RGB 数据。
- VzDS87：表示 DS87 相机，使用航空插头，同时提供 ToF+RGB 数据。
- VzDS77Lite：表示 DS77Lite 相机，使用 RJ45 接口，只提供 ToF 数据。
- VzDS77Pro：表示 DS77Pro 相机，使用航空插头，只提供 ToF 数据。
- VzDS77CLite：表示 DS77CLite 相机，使用 RJ45 接口，同时提供 ToF+RGB 数据。
- VzDS77CPro：表示 DS77CPro 相机，使用航空插头，同时提供 ToF+RGB 数据。

### 5.1.7. VzWorkMode

**功能：**

设备工作状态。

**枚举值：**

- VzActiveMode：表示设备处于主动工作状态。此时使用 API 打开相机后，设备会主动上传图像数据。
- VzHardwareTriggerMode：表示设备处于被动工作状态。此时使用 API 打开相机后，设备在硬件触发的时候，才会上传图像数据。
- VzSoftwareTriggerMode：表示设备处于被动工作状态。此时使用 API 打开相机后，设备在软件触发的时候，才会上传图像数据。

### 5.1.8. VzExposureControlMode

**功能：**

传感器的曝光模式。

**枚举值：**

- VzExposureControlMode_Auto：表示传感器使用自动曝光模式
- VzExposureControlMode_Manual：表示传感器使用手动曝光模式

## 5.2. Struct 数据类型

### 5.2.1. VzRGB888Pixel

**功能：**

彩色图像像素类型 RGB888。

_PS:不同型号产品可能不支持 RGB，如 DS77，请以 Include 中具体型号文件夹下定义为准。_

**成员：**

- uint8_t r：表示红色通道
- uint8_t g：表示绿色通道
- uint8_t b：表示蓝色通道

### 5.2.2. VzBGR888Pixel

**功能：**

彩色图像像素类型 BGR888。

_PS:不同型号产品可能不支持 RGB，如 DS77，请以 Include 中具体型号文件夹下定义为准。_

**成员：**

- uint8_t b：表示蓝色通道
- uint8_t g：表示绿色通道
- uint8_t r：表示红色通道

### 5.2.3. VzVector3f

**功能：**

3 维点坐标，单位为毫米。

**成员：**

- float x：表示 X 轴方向的坐标值
- float y：表示 Y 轴方向的坐标值
- float z：表示 Z 轴方向的坐标值

### 5.2.4. VzVector2u16

**功能：**

2 维点坐标。

**成员：**

- float x：表示 X 轴方向的坐标值
- float y：表示 Y 轴方向的坐标值

### 5.2.5. VzDepthVector3

**功能：**

深度图像的像素点表示。

**成员：**

- int depthX：表示图像坐标系下，X 轴方向的坐标值
- int depthY：表示图像坐标系下，Y 轴方向的坐标值
- VzDepthPixel depthZ：表示像素坐标（depthX，depthY）处的深度值，单位为毫米

### 5.2.6. VzSensorIntrinsicParameters

**功能：**

传感器的镜头内参和畸变参数。内参通常用于点云的计算，畸变参数用于图像反畸变算法使用。

SDK 中已经实现深度图像到点云的转换及图像反畸变的功能，请参考例程使用相关接口。

**成员：**

- double fx：Focal length x (pixel)
- double fy：Focal length y (pixel)
- double cx：Principal point x (pixel)
- double cy：Principal point y (pixel)
- double k1：Radial distortion coefficient, 1st-order
- double k2：Radial distortion coefficient, 2nd-order
- double p1：Tangential distortion coefficient
- double p2：Tangential distortion coefficient
- double k3：Radial distortion coefficient, 3rd-order
- double k4：Radial distortion coefficient, 4st-order
- double k5：Radial distortion coefficient, 5nd-order
- double k6：Radial distortion coefficient, 6rd-order

### 5.2.7. VzSensorExtrinsicParameters

**功能：**

相机外参 R 与 T，用于 depth 与 rgb 图像的对齐，参考公式如下:

![VzSensorExtrinsicParameters](pic/VzSensorExtrinsicParameters.png)

**成员：**

- double rotation[9]：3×3 的旋转矩阵
- double translation[3]：3×1 平移矩阵

### 5.2.8. VzFrame

**功能：**

图像信息。

**成员：**

- uint32_t frameIndex：表示图像帧索引号
- VzFrameType frameType：表示图像数据类型
- VzPixelFormat pixelFormat：表示像素类型
- uint8_t\* pFrameData：表示指向图像数据缓存的指针
- uint32_t dataLen：表示图像数据的长度，单位为字节
- float exposureTime：表示曝光时间，单位为微秒
- uint8_t depthRange：表示当前帧的深度范围，仅对深度图像有效
- uint16_t width：表示图像宽度
- uint16_t height：表示图像高度
- uint64_t deviceTimestamp：表示图像时间戳

### 5.2.9. VzFrameReady

**功能：**

图像数据是否就绪（1 代表就绪，0 代表未就绪）。

**枚举值：**

- uint32_t depth : 1：表示深度图像数据是否就绪
- uint32_t ir : 1：表示灰度图像数据是否就绪
- uint32_t color : 1：表示彩色图像数据是否就绪
- uint32_t transformedColor : 1：表示对齐到深度传感器空间的彩色图像是否就绪
- uint32_t transformedDepth : 1：表示对齐到彩色传感器空间的深度图像是否就绪
- uint32_t confidence : 1：表示激光强度图像数据是否就绪
- uint32_t reserved : 26：：预留位

### 5.2.10. VzDeviceInfo

**功能：**

设备信息。

**成员：**

- int SessionCount：表示设备中有几个深度传感器
- VzDeviceType devicetype：表示设备类型
- char uri[256]：表示设备的标识符
- char alias[64]：表示设备的别名
- char serialNumber[64]：表示设备的序列号
- char ip[17]：表示设备的 IP 地址
- VzConnectStatus status：表示设备连接状态

### 5.2.11. VzConfidenceFilterParams

**功能：**

置信度滤波参数。

**成员：**

- bool enable：表示滤波是否打开，true 代表打开，false 代表关闭
- int threshold：表示滤波阈值

### 5.2.12. VzFlyingPixelFilterParams

**功能：**

去飞点滤波参数。

**成员：**

- bool enable：表示滤波是否打开，true 代表打开，false 代表关闭
- int threshold：表示滤波阈值

### 5.2.13. VzSpatialFilterParams

**功能：**

空间滤波参数。

**成员：**

- bool enable：表示滤波是否打开，true 代表打开，false 代表关闭
- int validCount：表示滤波计算时使用的参考点个数
- int threshold：表示滤波阈值
- int doCount：表示滤波执行几遍

### 5.2.14. VzFillHoleFilterParams

**功能：**

补洞滤波参数。

**成员：**

- bool enable：表示滤波是否打开，true 代表打开，false 代表关闭
- int validCount：表示滤波计算时使用的参考点个数
- int threshold：表示滤波阈值
- int doCount：表示滤波执行几遍

### 5.2.15. VzExposureTimeParams

**功能：**

传感器曝光参数

**成员：**

- VzExposureControlMode mode：表示传感器曝光类型
- int exposureTime：表示传感器曝光时间，单位微秒
