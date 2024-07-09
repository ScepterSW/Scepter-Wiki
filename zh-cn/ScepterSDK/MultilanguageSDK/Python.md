# 3.1. Python

## 3.1.1. 基础介绍

Python SDK 目录结构如下：

![PythonContents](Python-asserts/01.png)

- API：主要包含 SDK 的通用头文件：Scepter_api.py，Scepter_define.py，Scepter_enums.py，Scepter_types.py。

- Samples：主要包含使用 ScepterSDK 开发的例程。

- README.md：SDK 的内容简介。

## 3.1.2. 项目配置

在运行 ScepterSDK 之前，请确保您的 Python 版本为 3.7.x 或更高版本，并已安装 ctypes、numpy 模块。在大多数 Python 发行版中，ctypes 都是作为内置模块存在的，因此我们无需额外安装。

```console
pip install numpy
```

使用 Scepter SDK 开发新的项目，需要使用英文路径。针对不同的操作系统，需要同时复制 SDK 中的 Python 文件夹和对应系统的文件夹。API 文件夹中的 Scepter_api.py 会自动读取相机的 libScepter_api.so 或 Scepter_api.dll 库文件。

```python
if system_ == 'linux':
   if machine_ == 'x86_64':
      os_info = os.uname()
      print('os_info:',type(os_info))
      system_info = os_info.version
      print('version:',system_info)
      if system_info.find('18.04') != -1 or system_info.find('20.04') != -1:
         libpath = (os.path.abspath(os.path.dirname(os.getcwd()) + os.path.sep + "../../../../BaseSDK/"))+"/Ubuntu18.04/Lib/libScepter_api.so"
         print(libpath)
         self.vz_cam_lib = cdll.LoadLibrary(libpath)
      else:
         libpath = (os.path.abspath(os.path.dirname(os.getcwd()) + os.path.sep + "../../../../BaseSDK/"))+"/Ubuntu16.04/Lib/libScepter_api.so"
         print(libpath)
         self.vz_cam_lib = cdll.LoadLibrary(libpath)
      elif machine_ == 'aarch64':
         libpath = (os.path.abspath(os.path.dirname(os.getcwd()) + os.path.sep + "../../../../BaseSDK/"))+"/AArch64/Lib/libScepter_api.so"
         print(libpath)
         self.vz_cam_lib = cdll.LoadLibrary(libpath)
   else:
      print('do not supported OS', system_, machine_)
      exit()
elif platform.system() == 'Windows':
   if machine_ == 'amd64':
      if architecture_ == '64bit':
         libpath = (os.path.abspath(os.path.dirname(os.getcwd()) + os.path.sep + "../../../../BaseSDK/"))+"/Windows/Bin/x64/Scepter_api.dll"
         print(libpath)
         elf.vz_cam_lib = cdll.LoadLibrary(libpath)
   else:
      libpath = (os.path.abspath(os.path.dirname(os.getcwd()) + os.path.sep + "../../../../BaseSDK/"))+"/Windows/Bin/x86/Scepter_api.dll"
      print(libpath)
      self.vz_cam_lib = cdll.LoadLibrary(libpath)
   else:
      print('do not supported OS', system_, machine_)
      exit()
else:
   print('do not supported OS', system_, machine_)
   exit()

```

## 3.1.3. 基础例程

基础例程介绍 SDK 的单个特性 API 接口的使用。为了使用户可以快速的熟悉使用，例程根据产品进行分类。

例程包含打开图像数据流、图像获取、软/硬触发、点云转换与保存等 API 接口的使用。

![PythonSamples](Python-asserts/02.png)

接下来，我们将详细介绍每个例程的功能。

```python
ColorExposureTimeSetGet                         #设置获取设备彩色传感器曝光时间
ColorResolutionChange                           #更改设备彩色传感器分辨率
DevHotPlugCallback                              #设置设备热插拔回调
DeviceConnectByIP                               #设置设备通过 IP 地址链接
DeviceConnectBySN                               #设置设备通过设备 SN 连接
DeviceHWTriggerMode                             #设置设备为硬触发模式
DeviceInfoGet                                   #获取设备 SN、IP 地址、固件版本信息
DeviceParamSetGet                               #获取设备内外参、畸变参数，设置、获取设备 GammaGain 值
DeviceSearchAndConnect                          #搜索并连接设备
DeviceSetParamsByJson                           #通过 Json 设置设备参数
DeviceStartStopStreaming                        #开始与停止设备数据流
DeviceSWTriggerMode                             #设置设备为软触发模式
FrameCaptureAndSave                             #捕获与保存设备图像
FrameViewer                                     #设备的OpenCV例程
MultiConnection                                 #多设备连接
IRGMMCorrectionSetGet                           #设置获取设备 ToF IR校正参数
PointCloudCaptureAndSave                        #捕获与保存点云
ToFExposureTimeSetGet                           #设置获取设备 ToF 曝光时间
ToFFiltersSetGet                                #设置获取设备 ToF 滤波开关
TransformColorImgToDepthSensorFrame             #将彩色图像对齐到设备的深度图像空间
TransformDepthImgToColorSensorFrame             #将深度图像对齐到设备的彩色图像空间
```

下面，我们以单个产品的单独例程为例，演示其编译运行的过程：

1. 根据实际产品选择对应的 sample，以 NYX650 产品编译 DeviceConnectBySN 为例

   ![PythonDeviceConnectBySN](Python-asserts/03.png)

2. 编译完成，调试运行。

   ```consle
   cd ScepterSDK\Python\Samples\NYX650\DeviceConnectBySN
   python DeviceConnectBySN.py
   ```

   结果如下图：

   ![PythonDeviceConnectBySNResult](Python-asserts/04.png)

## 3.1.4. OpenCV 例程

OpenCV 例程用于展示如何搭配第三方库使用 Scepter SDK。例程使用 OpenCV 的图像映射功能展示彩色深度图像、IR 与 Color 图像。

1. 安装 opencv-python 模块。

   ```console
   pip install opencv-python
   ```

2. 根据实际产品选择对应的 sample，以 NYX650 为例

   ![PythonOpenCV](Python-asserts/05.png)

3. 运行 OpenCV 显示例程

   ```consle
   cd ScepterSDK\Python\Samples\NYX650\FrameViewer
   python FrameViewer.py
   ```

   ![PythonOpenCVResult](Python-asserts/06.png)

## 3.1.5. API 参考

> 不同型号产品对应的枚举值个数可能不同，请以实际枚举值为准。

<!-- tabs:start -->

#### **Enum 数据类型**

### 3.1.5.1.1. ScFrameType

**功能：**

图像类型。

**枚举值：**

```python
class ScFrameType(Enum):
    SC_DEPTH_FRAME       = 0                                #表示深度图像类型，每像素16位，以毫米为单位
    SC_IR_FRAME          = 1                                #表示灰度图像类型，每像素8位
    SC_COLOR_FRAMEE      = 3                                #表示彩色图像类型，每像素24位，RGB/BGR格式
    SC_TRANSFORM_COLOR_IMG_TO_DEPTH_SENSOR_FRAME = 4        #表示映射到深度传感器空间的彩色图像类型，其中分辨率与深度图像的分辨率相同
                                                            #可以使用scSetTransformColorImgToDepthSensorEnabled()启用此帧类型
    SC_TRANSFORM_DEPTH_IMG_TO_COLOR_SENSOR_FRAME = 5        #表示映射到彩色传感器空间的深度图像类型，其中分辨率与彩色图像的分辨率相同。
                                                            #可以使用scSetTransformDepthImgToColorSensorEnabled()启用此帧类型
```

### 3.1.5.1.2. ScSensorType

**功能：**

传感器类型。

**枚举值：**

```python
class ScSensorType(Enum):
    SC_TOF_SENSOR = 0x01      #表示深度数据传感器
    SC_COLOR_SENSOR = 0x02    #表示彩色图像传感器
```

### 3.1.5.1.3. ScPixelFormat

**功能：**

图像数据的像素类型。

**枚举值：**

```python
class ScPixelFormat(Enum):
    SC_PIXEL_FORMAT_DEPTH_MM16      = 0   #表示每个像素数据为 16 位的深度值，单位为毫米
    SC_PIXEL_FORMAT_GRAY_8          = 2   #表示每个像素数据为 8 位的灰度值
    SC_PIXEL_FORMAT_RGB_888_JPEG    = 3   #表示通过JPEG解压缩，彩色图像像素格式，每个像素数据为 24 位的 RGB 值
    SC_PIXEL_FORMAT_BGR_888_JPEG    = 4   #表示通过JPEG解压缩，彩色图像像素格式，每个像素数据为 24 位的 BGR 值
    SC_PIXEL_FORMAT_RGB_888         = 5   #表示无压缩，彩色图像像素格式，每个像素数据为 24 位的 RGB 值
    SC_PIXEL_FORMAT_BGR_888         = 6   #表示无压缩，彩色图像像素格式，每个像素数据为 24 位的 BGR 值
    SC_PIXEL_FORMAT_RGB_565         = 7   #表示无压缩，彩色图像像素格式，每个像素数据为 16 位的 RGB 值
    SC_PIXEL_FORMAT_BGR_565         = 8   #表示无压缩，彩色图像像素格式，每个像素数据为 16 位的 BGR 值
```

### 3.1.5.1.4. ScReturnStatus

**功能：**

接口函数的返回值。

**枚举值：**

```python
class ScReturnStatus(Enum):
    SC_OK                           =  0     #表示调用成功
    SC_NO_DEVICE_CONNECTED          = -1     #表示当前无设备连接，或设备未正确连接。检查硬件连接或尝试拔下并重新插入电缆。
    SC_INVALID_DEVICE_INDEX         = -2     #表示传入的设备序号无效
    SC_DEVICE_POINTER_IS_NULL       = -3     #表示传入的设备指针为空
    SC_INVALID_FRAME_TYPE           = -4     #表示传入的图像类型无效
    SC_FRAME_POINTER_IS_NULL        = -5     #表示传入的图像指针为空
    SC_NO_PROPERTY_VALUE_GET        = -6     #表示无法获取当前属性值
    SC_NO_PROPERTY_VALUE_SET        = -7     #表示无法设置当前属性值
    SC_PROPERTY_POINTER_IS_NULL     = -8     #表示传入的指向存储属性值的缓存指针为空
    SC_PROPERTY_SIZE_NOT_ENOUGH     = -9     #表示传入的指向存储属性值的缓存空间不足
    SC_INVALID_DEPTH_RANGE          = -10    #表示传入的 depth range 无效
    SC_GET_FRAME_READY_TIME_OUT     = -11    #表示获取图像时超时
    SC_INPUT_POINTER_IS_NULL        = -12    #表示传入的指针为空
    SC_CAMERA_NOT_OPENED            = -13    #表示相机未打开
    SC_INVALID_CAMERA_TYPE          = -14    #表示传入的相机类型无效
    SC_INVALID_PARAMS               = -15    #表示传入的参数无效
    SC_CURRENT_VERSION_NOT_SUPPORT  = -16    #表示当前版本不支持
    SC_UPGRADE_IMG_ERROR            = -17    #表示升级相机固件失败
    SC_UPGRADE_IMG_PATH_TOO_LONG    = -18    #表示传入的相机固件路径长度太长（大于260）
    SC_UPGRADE_CALLBACK_NOT_SET     = -19    #表示未设置相机升级时的回调函数
    SC_PRODUCT_NOT_SUPPORT          = -20    #表示当前设备不支持此操作
    SC_NO_CONFIG_FOLDER             = -21    #表示未找到产品配置文件
    SC_WEB_SERVER_START_ERROR       = -22    #表示Web服务器启动/重新启动错误（IP或端口）
    SC_GET_OVER_STAY_FRAME          = -23    #表示从帧准备就绪到获取帧的时间超出1秒
    SC_CREATE_LOG_DIR_ERROR         = -24    #表示创建日志目录错误
    SC_CREATE_LOG_FILE_ERROR        = -25    #表示创建日志文件错误
    SC_NO_ADAPTER_CONNECTED         = -100   #表示电源适配器未连接
    SC_REINITIALIZED                = -101   #表示重复初始化
    SC_NO_INITIALIZED               = -102   #表示未做初始化
    SC_CAMERA_OPENED                = -103   #表示相机已经打开
    SC_CMD_ERROR                    = -104   #表示命令下发失败
    SC_CMD_SYNC_TIME_OUT            = -105   #表示命令发送成功，但是同步匹配失败
    SC_IP_NOT_MATCH                 = -106   #表示相机 IP 与主机 IP 不在同一网段
    SC_NOT_STOP_STREAM              = -107   #表示未调用SCStopStream关闭数据流
    SC_NOT_START_STREAM             = -108   #表示未调用scStartStream获取数据流
    SC_NOT_FIND_DRIVERS_FOLDER      = -109   #表示驱动程序目录不存在
    SC_CAMERA_OPENING               = -110   #表示相机已通过另一个SC_OpenDeviceByXXX API打开
    SC_CAMERA_OPENED_BY_ANOTHER_APP = -111   #表示相机已被其他应用程序打开
    ScRetOthers                     = -255   #表示其他错误
```

### 3.1.5.1.5. ScConnectStatus

**功能：**

设备连接状态。

**枚举值：**

```python
class ScConnectStatus(Enum):
    SC_LIMBO       = 0     #表示未知设备状态，无法尝试打开
    SC_CONNECTABLE = 1     #表示设备可连接状态，支持打开
    SC_OPENED      = 2     #表示设备已连接，无法再次打开
```

### 3.1.5.1.6. ScWorkMode

**功能：**

设备工作状态。

**枚举值：**

```python
class ScWorkMode(Enum):
    SC_ACTIVE_MODE           = 0x00    #表示设备处于主动工作状态。此时使用 API 打开相机后，设备会主动上传图像数据
    SC_HARDWARE_TRIGGER_MODE = 0x01    #表示设备处于被动工作状态。此时使用 API 打开相机后，设备在硬件触发的时候，才会上传图像数据
    SC_SOFTWARE_TRIGGER_MODE = 0x02    #表示设备处于被动工作状态。此时使用 API 打开相机后，设备在软件触发的时候，才会上传图像数据
```

### 3.1.5.1.7. ScExposureControlMode

**功能：**

传感器的曝光模式。

**枚举值：**

```python
class ScExposureControlMode(Enum):
    SC_EXPOSURE_CONTROL_MODE_AUTO   = 0    #表示传感器使用自动曝光模式
    SC_EXPOSURE_CONTROL_MODE_MANUAL = 1    #表示传感器使用手动曝光模式
```

#### **Struct 数据类型**

### 3.1.5.2.1. ScRGB888Pixel

**功能：**

彩色图像像素类型 RGB888。

**成员：**

```python
class ScRGB888Pixel(Structure):
    _pack_ = 1
    _fields_ = [("r", c_uint8),     #表示红色通道
                ("g", c_uint8),     #表示绿色通道
                ("b", c_uint8)]     #表示蓝色通道
```

### 3.1.5.2.2. ScBGR888Pixel

彩色图像像素类型 BGR888。

**成员：**

```python
class ScBGR888Pixel(Structure):
    _pack_ = 1
    _fields_ = [("b", c_uint8),     #表示蓝色通道
                ("g", c_uint8),     #表示绿色通道
                ("r", c_uint8)]     #表示红色通道
```

### 3.1.5.2.3. ScVector3f

**功能：**

3 维点坐标，单位为毫米。

**成员：**

```python
class ScVector3f(Structure):
    _pack_ = 1
    _fields_ = [("x", c_float),     #表示 X 轴方向的坐标值
                ("y", c_float),     #表示 Y 轴方向的坐标值
                ("z", c_float)]     #表示 Z 轴方向的坐标值
```

### 3.1.5.2.4. ScVector2u16

**功能：**

2 维点坐标。

**成员：**

```python
class ScVector2u16(Structure):
    _pack_ = 1
    _fields_ = [("x", c_uint16),    #表示 X 轴方向的坐标值
                ("y", c_uint16)]    #表示 Y 轴方向的坐标值
```

### 3.1.5.2.5. ScDepthVector3

**功能：**

深度图像的像素点表示。

**成员：**

```python
class ScDepthVector3(Structure):
    _pack_ = 1
    _fields_ = [("depthX", c_int),     #表示图像坐标系下，X 轴方向的坐标值
                ("depthY", c_int),     #表示图像坐标系下，Y 轴方向的坐标值
                ("depthZ", c_uint16)]  #表示像素坐标（depthX，depthY）处的深度值，单位为毫米
```

### 3.1.5.2.6. ScResolution

**功能：**

图像分辨率。

**成员：**

```python
class ScResolution(Structure):
    _pack_ = 1
    _fields_ = [("width", c_int),      #表示图像的宽度
                ("height", c_int)]     #表示图像的高度
```

### 3.1.5.2.7. ScResolutionList

**功能：**

支持的图像分辨率。

**成员：**

```python
class ScResolutionList(Structure):
    _pack_ = 1
    _fields_ = [("count", c_int),                     #表示支持的图像分辨率的数量
                ("resolution", ScResolution * 6)]     #表示支持的图像分辨率的信息
```

### 3.1.5.2.8. ScSensorIntrinsicParameters

**功能：**

传感器的镜头内参和畸变参数。内参通常用于点云的计算，畸变参数用于图像反畸变算法使用。

SDK 中已经实现深度图像到点云的转换及图像反畸变的功能，请参考例程使用相关接口。

**成员：**

```python
class ScSensorIntrinsicParameters(Structure):
    _pack_ = 1
    _fields_ = [("fx", c_double),      #x方向的焦距，单位为像素
                ("fy", c_double),      #y方向的焦距，单位为像素
                ("cx", c_double),      #主点的x坐标，图像的中心，单位为像素
                ("cy", c_double),      #主点的y坐标，图像的中心，单位为像素
                ("k1", c_double),      #径向畸变, 1st
                ("k2", c_double),      #径向畸变, 2nd
                ("p1", c_double),      #轴向畸变
                ("p2", c_double),      #轴向畸变
                ("k3", c_double),      #径向畸变, 3rd
                ("k4", c_double),      #径向畸变, 4st
                ("k5", c_double),      #径向畸变, 5nd
                ("k6", c_double)]      #径向畸变, 6rd
```

### 3.1.5.2.9. ScSensorExtrinsicParameters

**功能：**

相机外参 R 与 T，用于 depth 与 rgb 图像的对齐，参考公式如下:

![ScSensorExtrinsicParameters](Python-asserts/07.png)

**成员：**

```python
class ScSensorExtrinsicParameters(Structure):
    _pack_ = 1
    _fields_ = [("rotation", c_double * 9),        #3×3 的旋转矩阵
                ("translation", c_double * 3)]     #3×1 平移矩阵
```

### 3.1.5.2.10. ScTimeStamp

**功能：**

表示图像时间戳。

**成员：**

```python
class ScTimeStamp(Structure):
    _pack_ = 1
    _fields_ = [("tm_sec", c_uint16),     #秒
                ("tm_min", c_uint16),     #分钟
                ("tm_hour", c_uint16),    #小时
                ("tm_msec", c_uint16)]    #毫秒
```

### 3.1.5.2.11. ScFrame

**功能：**

图像信息。

**成员：**

```python
class ScFrame(Structure):
    _pack_ = 1
    _fields_ = [("frameIndex", c_uint32),             #表示图像帧索引号
                ("frameType", c_int32),               #表示图像数据类型
                ("pixelFormat", c_int32),             #表示像素类型
                ("pFrameData", POINTER(c_uint8)),     #表示指向图像数据缓存的指针
                ("dataLen", c_uint32),                #表示图像数据的长度，单位为字节
                ("exposureTime", c_float),            #表示曝光时间，单位为毫秒
                ("depthRange", c_uint8),              #表示当前帧的深度范围，仅对深度图像有效
                ("width", c_uint16),                  #表示图像宽度
                ("height", c_uint16),                 #表示图像高度
                ("hardwaretimestamp", c_uint64)]      #表示帧在设备上生成时的时间戳，不包括帧处理和传输时间
```

### 3.1.5.2.12. ScFrameReady

**功能：**

图像数据是否就绪（1 代表就绪，0 代表未就绪）。

**枚举值：**

```python
class ScFrameReady(Structure):
    _pack_ = 1
    _fields_ = [("depth", c_uint, 1),                 #表示深度图像数据是否就绪
                ("ir", c_uint, 1),                    #表示灰度图像数据是否就绪
                ("color", c_uint, 1),                 #表示彩色图像数据是否就绪
                ("transformedColor", c_uint, 1),      #表示对齐到深度传感器空间的彩色图像是否就绪
                ("transformedDepth", c_uint, 1),      #表示对齐到彩色传感器空间的深度图像是否就绪
                ("reserved", c_uint, 27)]             #预留位
```

### 3.1.5.2.13. ScDeviceInfo

**功能：**

设备信息。

**成员：**

```python
class ScDeviceInfo(Structure):
    _pack_ = 1
    _fields_ = [("productName", c_char * 64),      #表示设备的产品名称
                ("serialNumber", c_char * 64),     #表示设备的序列号
                ("ip", c_char * 17),               #表示设备的 IP 地址
                ("status", c_int32)]               #表示设备连接状态
```

### 3.1.5.2.14. ScConfidenceFilterParams

**功能：**

置信度滤波参数。

**成员：**

```python
class ScConfidenceFilterParams(Structure):
    _pack_ = 1
    _fields_ = [("threshold", c_int32),      #表示滤波阈值，[1，100]，数值越大，过滤效果越明显，过滤掉的点数越多
                ("enable", c_bool)]          #表示滤波是否打开，true 代表打开，false 代表关闭
```

### 3.1.5.2.15. ScFlyingPixelFilterParams

**功能：**

去飞点滤波参数。

**成员：**

```python
class ScFlyingPixelFilterParams(Structure):
    _pack_ = 1
    _fields_ = [("threshold", c_int32),      #表示滤波阈值，[0，16]，数值越大，过滤效果越明显，过滤掉的点数越多
                ("enable", c_bool)]          #表示滤波是否打开，true 代表打开，false 代表关闭
```

### 3.1.5.2.16. ScTimeFilterParams

**功能：**

时间滤波参数。

**成员：**

```python
class ScTimeFilterParams(Structure):
    _pack_ = 1
    _fields_ = [("threshold", c_int32),      #表示滤波阈值，[1，6]，值越大，滤波效果越明显，点云抖动越小
                ("enable", c_bool)]          #表示滤波是否打开，true 代表打开，false 代表关闭
```

### 3.1.5.2.17. ScIRGMMCorrectionParams

**功能：**

IR gain 值校正参数。

**成员：**

```python
class ScIRGMMCorrectionParams(Structure):
    _pack_ = 1
    _fields_ = [("threshold", c_int32),      #表示滤波阈值，[0，100]，数值越大，校正效果越明显
                ("enable", c_bool)]          #表示滤波是否打开，true 代表打开，false 代表关闭
```

#### **API 介绍**

### 3.1.5.3.1. scGetSDKVersion

**函数原型：**

```python
def scGetSDKVersion(self):
   tmp = c_char * 64
   version = tmp()
   return self.sc_cam_lib.scGetSDKVersion(version, 63),version.value
```

**函数功能：**

获取 SDK 的版本号：x.x.x

**函数参数：**

无

**返回值：**

**version.value**：SDK 版本号

### 3.1.5.3.2. scGetDeviceCount

**函数原型：**

```python
def scGetDeviceCount(self, scanTime = c_uint32(33)):
   count = c_int()
   self.sc_cam_lib.scGetDeviceCount(byref(count), scanTime)
   return count.value
```

**函数功能：**

获取已连接的设备数目

**函数参数：**

byref(count)：在该变量中返回设备数量

scanTime：单位为毫秒，数值范围为（0，65535）。
当设备计数不为 0 时，API 立即返回。
当设备计数为 0 时，除非设备计数不为 0，否则 API 最多等待等待时间（ms）。

**返回值：**

**count.value**：设备数量

### 3.1.5.3.3. GetDeviceInfoList

**函数原型：**

```python
def scGetDeviceInfoList(self, cam_count = 1):
   tmp  = ScDeviceInfo* cam_count
   device_infolist = tmp()
   return self.sc_cam_lib.scGetDeviceInfoList(cam_count, device_infolist),device_infolist
```

**函数功能：**

获取 deviceCount 个数的设备信息列表

**函数参数：**

cam_count：需要获取信息列表的设备个数

[device_infolist](#_315213-scdeviceinfo)：返回设备信息列表，其应该指向大小为 sizeof(ScDeviceInfo)\*deviceCount 大小的缓存

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

[**device_infolist**](#_315213-scdeviceinfo)：返回设备信息列表，其应该指向大小为 sizeof(ScDeviceInfo)\*deviceCount 大小的缓存

### 3.1.5.3.4. scOpenDeviceBySN

**函数原型：**

```python
def scOpenDeviceBySN(self,  SN=c_char_p()):
   if SN:
      return self.sc_cam_lib.scOpenDeviceBySN(SN, byref(self.device_handle))
   else:
      return ScReturnStatus.SC_INPUT_POINTER_IS_NULL
```

**函数功能：**

使用设备标识符打开设备

**函数参数：**

SN：设备标识符

byref(self.device_handle)： 打开设备成功后，返回的设备句柄

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

### 3.1.5.3.5. scOpenDeviceByIP

**函数原型：**

```python
def scOpenDeviceByIP(self,  ip=c_char_p()):
   if ip:
      return self.sc_cam_lib.scOpenDeviceByIP(ip, byref(self.device_handle))
   else:
      return ScReturnStatus.SC_INPUT_POINTER_IS_NULL, 0
```

**函数功能：**

使用设备 IP 地址打开设备

**函数参数：**

ip：设备的 IP 地址

byref(self.device_handle)： 打开设备成功后，返回的设备句柄

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

### 3.1.5.3.6. scCloseDevice

**函数原型：**

```python
def scCloseDevice(self):
   return self.sc_cam_lib.scCloseDevice(byref(self.device_handle))
```

**函数功能：**

关闭设备

**函数参数：**

byref(self.device_handle)： 要关闭设备的句柄

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

### 3.1.5.3.7. scStartStream

**函数原型：**

```python
def scStartStream(self):
   return self.sc_cam_lib.scStartStream(self.device_handle)
```

**函数功能：**

打开数据流

**函数参数：**

self.device_handle：要打开数据流的设备的句柄

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

### 3.1.5.3.8. scStopStream

**函数原型：**

```python
def scStopStream(self):
   return self.sc_cam_lib.scStopStream(self.device_handle)
```

**函数功能：**

关闭数据流

**函数参数：**

self.device_handle：要关闭数据流的设备的句柄

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

### 3.1.5.3.9. scGetFrameReady

**函数原型：**

```python
def scGetFrameReady(self,waitTime = c_uint16(33)):
   frameready = ScFrameReady()
   if not self.device_handle:
      return -3, frameready
   return self.sc_cam_lib.scGetFrameReady(self.device_handle, waitTime, byref(frameready)), frameready
```

**函数功能：**

获取图像就绪状态。调用函数 scGetFrame 前必须调用此函数，否则无法获取图像。

**函数参数：**

self.device_handle： 设备句柄

waitTime：允许等待图像就绪的超时时间(ms)，取值范围为(0，65535)。此值与图像的帧率有关，建议值设置为 2\*1000/fps。例如当前的帧率为 20，则建议设置 waitTime 为 2 \* 1000 / 20 = 100。如果设置 waitTime 为 40，则调用函数时可能返回 ScRetGetFrameReadyTimeOut。

[byref(frameready)](#_315212-scframeready)：返回图像的就绪状态

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

[**frameready**](#_315212-scframeready)：返回图像的就绪状态

### 3.1.5.3.10. scGetFrame

**函数原型：**

```python
def scGetFrame(self,  frametype = ScFrameType.SC_DEPTH_FRAME):
   Scframe = ScFrame()
   return self.sc_cam_lib.scGetFrame(self.device_handle, frametype.value, byref(Scframe)), Scframe
```

**函数功能：**

获取指定图像类型的图像数据。调用此函数前必须调用 scGetFrameReady。

**函数参数：**

self.device_handle：设备句柄

[frametype.value](#_31511-scframetype)：待获取图像的类型

[byref(Scframe)](#_315211-scframe)：返回的图像数据

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

[**Scframe**](#_315211-scframe)：返回的图像数据

### 3.1.5.3.11. scSetWorkMode

**函数原型：**

```python
def scSetWorkMode(self,  mode = ScWorkMode.SC_ACTIVE_MODE):
   return self.sc_cam_lib.scSetWorkMode(self.device_handle, mode.value)
```

**函数功能：**

设置相机的工作模式

**函数参数：**

self.device_handle：设备句柄

[mode.value](#_31516-scworkmode)：要设置的工作模式，对于 ActiveMode ，将时间过滤器的默认值设置为 True ，对于 SlaveMode ，将时间过滤器的默认值设置为 False

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

### 3.1.5.3.12. scGetWorkMode

**函数原型：**

```python
def scGetWorkMode(self):
   mode = ScWorkMode(0)
   return self.sc_cam_lib.scGetWorkMode(self.device_handle, byref(mode)), mode
```

**函数功能：**

获取相机的工作模式

**函数参数：**

self.device_handle：设备句柄

[byref(mode)](#_31516-scworkmode)：获取到的设备的工作模式

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

[**mode**](#_31516-scworkmode)：获取到的设备的工作模式

### 3.1.5.3.13. scSoftwareTriggerOnce

**函数原型：**

```python
def scSoftwareTriggerOnce(self):
   return self.sc_cam_lib.scSoftwareTriggerOnce(self.device_handle)
```

**函数功能：**

执行一次软件触发，仅当相机处于 SC_SOFTWARE_TRIGGER_MODE 时有效

**函数参数：**

self.device_handle：设备句柄

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

### 3.1.5.3.14. scRebootDevie

**函数原型：**

```python
def scRebootDevie(self):
   return self.sc_cam_lib.scRebootDevie(self.device_handle)
```

**函数功能：**

重启设备

**函数参数：**

self.device_handle：设备句柄

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

### 3.1.5.3.15. scGetSensorIntrinsicParameters

**函数原型：**

```python
def scGetSensorIntrinsicParameters(self, sensorType = ScSensorType.SC_TOF_SENSOR):
   CameraParameters = ScSensorIntrinsicParameters()
   return self.sc_cam_lib.scGetSensorIntrinsicParameters(self.device_handle, sensorType.value, byref(CameraParameters)), CameraParameters
```

**函数功能：**

获取传感器镜头的内参

**函数参数：**

self.device_handle：设备句柄

[sensorType.value](#_31512-scsensortype)：传感器类型

[byref(CameraParameters)](#_31528-scsensorintrinsicparameters)：返回传感器镜头的内参

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

[**CameraParameters**](#_31528-scsensorintrinsicparameters)：返回传感器镜头的内参

### 3.1.5.3.16. scGetSensorExtrinsicParameters

**函数原型：**

```python
def scGetSensorExtrinsicParameters(self):
   CameraExtrinsicParameters = ScSensorExtrinsicParameters()
   return self.sc_cam_lib.scGetSensorExtrinsicParameters(self.device_handle, byref(CameraExtrinsicParameters)), CameraExtrinsicParameters
```

**函数功能：**

获取设备的外参

**函数参数：**

self.device_handle：设备句柄

[byref(CameraExtrinsicParameters)](#_31529-scsensorextrinsicparameters)：返回设备的外参

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

[**CameraExtrinsicParameters**](#_31529-scsensorextrinsicparameters)：返回设备的外参

### 3.1.5.3.17. scGetFirmwareVersion

**函数原型：**

```python
def scGetFirmwareVersion(self):
   tmp = c_char * 64
   fw = tmp()
   return self.sc_cam_lib.scGetFirmwareVersion(self.device_handle, fw, 63),fw.value
```

**函数功能：**

获取设备的固件版本

**函数参数：**

self.device_handle：设备句柄

fw：返回设备的固件版本

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

**fw.value**：返回设备的固件版本

### 3.1.5.3.18. scGetDeviceMACAddress

**函数原型：**

```python
def scGetDeviceMACAddress(self):
   tmp = c_char * 18
   mac = tmp()
   return self.sc_cam_lib.scGetDeviceMACAddress(self.device_handle, mac), mac.value
```

**函数功能：**

获取设备的 MAC 地址

**函数参数：**

self.device_handle：设备句柄

mac：返回设备的 MAC 地址，其默认是一个字节长度为 18，以‘\0’结尾的字符串

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

**mac.value**：返回设备的 MAC 地址，其默认是一个字节长度为 18，以‘\0’结尾的字符串

### 3.1.5.3.19. scSetIRGMMGain

**函数原型：**

```python
def scSetIRGMMGain(self, gmmgain = c_uint8(20)):
   return self.sc_cam_lib.scSetIRGMMGain(self.device_handle, gmmgain)
```

**函数功能：**

设置 IR 图像的数字增益

**函数参数：**

self.device_handle：设备句柄

gmmgain：要设置给设备的 IR 增益值

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

### 3.1.5.3.20. scGetIRGMMGain

**函数原型：**

```python
def scGetIRGMMGain(self):
   gmmgain = c_uint8(1)
   return self.sc_cam_lib.scGetIRGMMGain(self.device_handle, byref(gmmgain)), gmmgain.value
```

**函数功能：**

获取 IR 图像的数字增益

**函数参数：**

self.device_handle：设备句柄

byref(gmmgain)：返回设备的 IR 增益值

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

**gmmgain.value**：返回设备的 IR 增益值

### 3.1.5.3.21. scSetIRGMMCorrection

**函数原型：**

```python
def scSetIRGMMCorrection(self, params = ScIRGMMCorrectionParams()):
   return self.sc_cam_lib.scSetIRGMMCorrection(self.device_handle, params)
```

**函数功能：**

设置设备上的 IR Gamma 校正的值

**函数参数：**

self.device_handle：设备句柄

[params](#_315217-scirgmmcorrectionparams)：IR Gamma 校正的值

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

### 3.1.5.3.22. scGetIRGMMCorrection

**函数原型：**

```python
def scGetIRGMMCorrection(self):
   params = ScIRGMMCorrectionParams()
   return self.sc_cam_lib.scGetIRGMMCorrection(self.device_handle, byref(params)), params
```

**函数功能：**

获取设备上的 IR Gamma 校正的值

**函数参数：**

self.device_handle：设备句柄

[byref(params)](#_315217-scirgmmcorrectionparams)：IR Gamma 校正的值

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

[**params**](#_315217-scirgmmcorrectionparams)：IR Gamma 校正的值

### 3.1.5.3.23. scSetColorPixelFormat

**函数原型：**

```python
def scSetColorPixelFormat(self,pixelFormat=ScPixelFormat.SC_PIXEL_FORMAT_BGR_888_JPEG):
   return self.sc_cam_lib.scSetColorPixelFormat(self.device_handle, pixelFormat)
```

**函数功能：**

设置彩色图像的像素格式，目前仅支持 RGB 和 BGR 格式

**函数参数：**

self.device_handle：设备句柄

[pixelFormat](#_31513-scpixelformat)：要设置的彩色图像的像素格式

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

### 3.1.5.3.24. scSetColorResolution

**函数原型：**

```python
def scSetColorResolution(self, w = c_int32(1600), h = c_int32(1200)):
   return self.sc_cam_lib.scSetColorResolution(self.device_handle, w, h)
```

**函数功能：**

设置彩色图像的分辨率

**函数参数：**

self.device_handle：设备句柄

w：图像的宽

h：图像的高

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

### 3.1.5.3.25. scGetColorResolution

**函数原型：**

```python
def scGetColorResolution(self):
   w = c_int32(1600)
   h = c_int32(1200)
   return self.sc_cam_lib.scGetColorResolution(self.device_handle, byref(w), byref(h)), w, h
```

**函数功能：**

获取彩色图像的分辨率

**函数参数：**

self.device_handle：设备句柄

byref(w)：返回彩色图像的图像宽

byref(h)：返回彩色图像的图像高

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

**w**：返回彩色图像的图像宽

**h**：返回彩色图像的图像高

### 3.1.5.3.26. scSetFrameRate

**函数原型：**

```python
def scSetFrameRate(self, value = c_uint8(30)):
   return self.sc_cam_lib.scSetFrameRate(self.device_handle, value)
```

**函数功能：**

设置设备的图像帧率，同时对深度和彩色图像生效。此接口是同步接口，耗时较长，大约需要 500ms

**函数参数：**

self.device_handle：设备句柄

value：要设置的目标帧率

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

### 3.1.5.3.27. scGetFrameRate

**函数原型：**

```python
def scGetFrameRate(self):
   value = c_uint8(1)
   return self.sc_cam_lib.scGetFrameRate(self.device_handle, byref(value)), value.value
```

**函数功能：**

获取设备的图像帧率

**函数参数：**

self.device_handle：设备句柄

byref(value)：返回设备的图像帧率

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

**value.value**：返回设备的图像帧率

### 3.1.5.3.28. scSetExposureControlMode

**函数原型：**

```python
def scSetExposureControlMode(self, sensorType = ScSensorType.SC_TOF_SENSOR, mode = ScExposureControlMode.SC_EXPOSURE_CONTROL_MODE_MANUAL):
   return self.sc_cam_lib.scSetExposureControlMode(self.device_handle, sensorType.value, mode.value)
```

**函数功能：**

设置传感器的曝光模式

**函数参数：**

self.device_handle：设备句柄

[sensorType.value](#_31512-scsensortype)：要设置曝光模式的传感器类型

[mode.value](#_31517-scexposurecontrolmode)：要设置的曝光模式

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

### 3.1.5.3.29. scSetExposureTime

**函数原型：**

```python
def scSetExposureTime(self, sensorType = ScSensorType.SC_TOF_SENSOR, params = c_int32(0)):
   return self.sc_cam_lib.scSetExposureTime(self.device_handle, sensorType.value, params)
```

**函数功能：**

设置传感器的曝光时间

深度传感器，只支持在手动曝光模式下，设置曝光时间

彩色传感器，支持在自动曝光模式下，设置最大曝光时间；支持在手动曝光模式下，设置曝光时间

**函数参数：**

self.device_handle：设备句柄

[sensorType.value](#_31512-scsensortype)：要获取曝光时间的传感器类型

params：要设置的曝光时间参数

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

### 3.1.5.3.30. scGetExposureTime

**函数原型：**

```python
def scGetExposureTime(self, sensorType = ScSensorType.SC_TOF_SENSOR):
   params = c_int32(0)
   return self.sc_cam_lib.scGetExposureTime(self.device_handle, sensorType.value, byref(params)), params
```

**函数功能：**

获取传感器的曝光时间

**函数参数：**

self.device_handle：设备句柄

[sensorType.value](#_31512-scsensortype)：要获取曝光时间的传感器类型

byref(params)：返回获取的曝光时间参数

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

**params**：返回获取的曝光时间参数

### 3.1.5.3.31. scSetTimeFilterParams

**函数原型：**

```python
def scSetTimeFilterParams(self, params = ScTimeFilterParams()):
   return self.sc_cam_lib.scSetTimeFilterParams(self.device_handle, params)
```

**函数功能：**

设置深度图像的时域滤波参数

**函数参数：**

self.device_handle：设备句柄

[params](#_315216-sctimefilterparams)：指向存储返回值的变量的指针

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

### 3.1.5.3.32. scGetTimeFilterParams

**函数原型：**

```python
def scGetTimeFilterParams(self):
   params = ScTimeFilterParams()
   return self.sc_cam_lib.scGetTimeFilterParams(self.device_handle, byref(params)),params
```

**函数功能：**

获取深度图像的时域滤波参数

**函数参数：**

self.device_handle：设备句柄

[params](#_315216-sctimefilterparams)：指向存储返回值的变量的指针

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

### 3.1.5.3.33. scSetConfidenceFilterParams

**函数原型：**

```python
def scSetConfidenceFilterParams(self, params = ScConfidenceFilterParams()):
   return self.sc_cam_lib.scSetConfidenceFilterParams(self.device_handle, params)
```

**函数功能：**

设置深度图像的置信度滤波参数

**函数参数：**

self.device_handle：设备句柄

[params](#_315214-scconfidencefilterparams)：指向存储返回值的变量的指针

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

### 3.1.5.3.34. scGetConfidenceFilterParams

**函数原型：**

```python
def scGetConfidenceFilterParams(self):
   params = ScConfidenceFilterParams()
   return self.sc_cam_lib.scGetConfidenceFilterParams(self.device_handle, byref(params)),params
```

**函数功能：**

获取深度图像的置信度滤波参数

**函数参数：**

self.device_handle：设备句柄

[byref(params)](#_315214-scconfidencefilterparams)：指向存储返回值的变量的指针

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

[**params**](#_315214-scconfidencefilterparams)：指向存储返回值的变量的指针

### 3.1.5.3.35. scSetFlyingPixelFilterParams

**函数原型：**

```python
def scSetFlyingPixelFilterParams(self, params = ScFlyingPixelFilterParams()):
   return self.sc_cam_lib.scSetFlyingPixelFilterParams(self.device_handle, params)
```

**函数功能：**

设置深度图像的去飞点滤波参数

**函数参数：**

self.device_handle：设备句柄

[params](#_315215-scflyingpixelfilterparams)：滤波参数

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

### 3.1.5.3.36. scGetFlyingPixelFilterParams

**函数原型：**

```python
def scGetFlyingPixelFilterParams(self):
   params = ScFlyingPixelFilterParams()
   return self.sc_cam_lib.scGetFlyingPixelFilterParams(self.device_handle, byref(params)),params
```

**函数功能：**

获取深度图像的去飞点滤波参数

**函数参数：**

self.device_handle：设备句柄

[byref(params)](#_315215-scflyingpixelfilterparams)：滤波参数

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

[**params**](#_315215-scflyingpixelfilterparams)：滤波参数

### 3.1.5.3.37. scSetFillHoleFilterEnabled

**函数原型：**

```python
def scSetFillHoleFilterEnabled(self, enable = c_bool(True)):
   return self.sc_cam_lib.scSetFillHoleFilterEnabled(self.device_handle, enable)
```

**函数功能：**

设置深度图像的补洞滤波开启关闭

**函数参数：**

self.device_handle：设备句柄

enable：true 开启，false 关闭

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

### 3.1.5.3.38. scGetFillHoleFilterEnabled

**函数原型：**

```python
    def scGetFillHoleFilterEnabled(self):
        enable = c_bool(True)
        return self.sc_cam_lib.scGetFillHoleFilterEnabled(self.device_handle, byref(enable)),enable.value
```

**函数功能：**

获取深度图像的补洞滤波开启关闭

**函数参数：**

self.device_handle：设备句柄

byref(enable)：true 开启，false 关闭

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

**enable.value**：true 开启，false 关闭

### 3.1.5.3.39. scSetSpatialFilterEnabled

**函数原型：**

```python
def scSetSpatialFilterEnabled(self, enable = c_bool(True)):
   return self.sc_cam_lib.scSetSpatialFilterEnabled(self.device_handle, enable)
```

**函数功能：**

设置深度图像的空间滤波开启关闭

**函数参数：**

self.device_handle：设备句柄

enable：true 开启，false 关闭

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

### 3.1.5.3.40. scGetSpatialFilterEnabled

**函数原型：**

```python
def scGetSpatialFilterEnabled(self):
   enable = c_bool(True)
   return self.sc_cam_lib.scGetSpatialFilterEnabled(self.device_handle, byref(enable)),enable.value
```

**函数功能：**

设置深度图像的空间滤波开启关闭

**函数参数：**

self.device_handle：设备句柄

byref(enable)：true 开启，false 关闭

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

**enable.value**：true 开启，false 关闭

### 3.1.5.3.41. scSetTransformColorImgToDepthSensorEnabled

**函数原型：**

```python
def scSetTransformColorImgToDepthSensorEnabled(self, enabled = c_bool(True)):
   return self.sc_cam_lib.scSetTransformColorImgToDepthSensorEnabled(self.device_handle,  enabled)
```

**函数功能：**

设置彩色图像对齐到深度相机空间的开关，只有带彩色传感器的设备才支持此操作。如果打开开关，则调用 scGetFrameReady 时，ScFrameReady.transformedColor 的值为 1，然后调用 scGetFrame 可以得到 ScTransformColorImgToDepthSensorFrame 类型的彩色图像，其大小与深度图像大小相同。

**函数参数：**

self.device_handle：设备句柄

enabled：true 打开对齐，false 关闭对齐

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

### 3.1.5.3.42. scGetTransformColorImgToDepthSensorEnabled

**函数原型：**

```python
def scGetTransformColorImgToDepthSensorEnabled(self):
   enabled = c_bool(True)
   return self.sc_cam_lib.scGetTransformColorImgToDepthSensorEnabled(self.device_handle,  byref(enabled)),enabled
```

**函数功能：**

获取彩色图像对齐到深度相机空间的开关状态

**函数参数：**

self.device_handle：设备句柄

byref(enabled)：返回开关状态

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

**enabled**：返回开关状态

### 3.1.5.3.43. scSetTransformDepthImgToColorSensorEnabled

**函数原型：**

```python
def scSetTransformDepthImgToColorSensorEnabled(self, enabled = c_bool(True)):
   return self.sc_cam_lib.scSetTransformDepthImgToColorSensorEnabled(self.device_handle,  enabled)
```

**函数功能：**

设置深度图像对齐到彩色相机空间的开关，只有带彩色传感器的设备才支持此操作。如果打开开关，则调用 scGetFrameReady 时，ScFrameReady.transformedDepth 的值为 1，然后调用 scGetFrame 可以得到 ScTransformDepthImgToColorSensorFrame 类型的深度图像，其大小与彩色图像大小相同。

**函数参数：**

self.device_handle：设备句柄

enabled：true 打开对齐，false 关闭对齐

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

### 3.1.5.3.44. scGetTransformDepthImgToColorSensorEnabled

**函数原型：**

```python
def scGetTransformDepthImgToColorSensorEnabled(self):
   enabled = c_bool(True)
   return self.sc_cam_lib.scGetTransformDepthImgToColorSensorEnabled(self.device_handle,  byref(enabled)),enabled
```

**函数功能：**

获取深度图像对齐到彩色相机空间的开关状态

**函数参数：**

self.device_handle：设备句柄

byref(enabled)：返回开关状态

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

**enabled**：返回开关状态

### 3.1.5.3.45. scConvertDepthFrameToPointCloudVector

**函数原型：**

```python
def scConvertDepthFrameToPointCloudVector(self, depthFrame = ScFrame()):
   len = depthFrame.width*depthFrame.height
   tmp =ScVector3f*len
   pointlist = tmp()
   return self.sc_cam_lib.scConvertDepthFrameToPointCloudVector(self.device_handle, byref(depthFrame) ,pointlist),pointlist
```

**函数功能：**

把传入的深度图像转换为世界坐标系点集合，转换后的世界坐标系点集合的大小为 ScFrame.width \* ScFrame.height，支持 ScDepthFrame 和 ScTransformDepthImgToColorSensorFrame 图像

**函数参数：**

self.device_handle：设备句柄

[byref(depthFrame)](#_315211-scframe)：深度图像

[pointlist](#_31523-scvector3f)：转换后点云的坐标点的集合

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

[**pointlist**](#_31523-scvector3f)：转换后点云的坐标点的集合

### 3.1.5.3.46. scSetHotPlugStatusCallback

**函数原型：**

```python
def scSetHotPlugStatusCallback(self,callbackfunc= c_void_p):
   callbackFunc_= ctypes.CFUNCTYPE(c_void_p,POINTER(ScDeviceInfo),c_int32)(callbackfunc)
   gCallbackFuncList.append(callbackFunc_)
   return self.sc_cam_lib.scSetHotPlugStatusCallback(callbackFunc_)
```

**函数功能：**

设置设备热拔插状态回调函数

**函数参数：**

callbackFunc\_： 回调函数

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

### 3.1.5.3.47. scGetMaxExposureTime

**函数原型：**

```python
def scGetMaxExposureTime(self, sensorType = ScSensorType.SC_COLOR_SENSOR):
   tmp = c_int32(1000)
   return self.sc_cam_lib.scGetMaxExposureTime(self.device_handle, sensorType.value, byref(tmp)), tmp
```

**函数功能：**

获取传感器的最大曝光时间

**函数参数：**

self.device_handle：设备句柄

[sensorType.value](#_31512-scsensortype)：要获取曝光时间的传感器类型

byref(tmp)：返回获取的最大曝光时间，在不同的帧率下，最大曝光时间有所不同

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

**tmp**：返回获取的最大曝光时间，在不同的帧率下，最大曝光时间有所不同

### 3.1.5.3.48. scSetParamsByJson

**函数原型：**

```python
def scSetParamsByJson(self, imgpath):
   pimgpath = (c_char * 1000)(*bytes(imgpath, 'utf-8'))
   return self.sc_cam_lib.scSetParamsByJson(self.device_handle,  byref(pimgpath))
```

**函数功能：**

从配置文件设置相机的参数

**函数参数：**

self.device_handle：设备句柄

byref(pimgpath)：配置文件路径

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

### 3.1.5.3.49. scSetColorGain

**函数原型：**

```python
def scSetColorGain(self, params = c_float(1.0)):
   return self.sc_cam_lib.scSetColorGain(self.device_handle,  params)
```

**函数功能：**

在手动曝光模式中，设置彩色传感器曝光模式的颜色增益

**函数参数：**

self.device_handle：设备句柄

params：彩色传感器的颜色增益值。不同的产品具有不同的范围，请参考产品说明书

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

### 3.1.5.3.50. scGetColorGain

**函数原型：**

```python
def scGetColorGain(self):
   tmp = c_float*1
   params = tmp()
   return self.sc_cam_lib.scGetColorGain(self.device_handle,  params), params
```

**函数功能：**

获取彩色传感器曝光模式的颜色增益

**函数参数：**

self.device_handle：设备句柄

params：彩色传感器的颜色增益值。不同的产品具有不同的范围，请参考产品说明书

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

**params**：彩色传感器的颜色增益值。不同的产品具有不同的范围，请参考产品说明书

### 3.1.5.3.51. scSetAutoExposureTime

**函数原型：**

```python
def scSetAutoExposureTime(self, params = c_int32(0)):
   return self.sc_cam_lib.scSetColorAECMaxExposureTime(self.device_handle, params)
```

**函数功能：**

设置彩色传感器在自动曝光模式下的最大曝光时间。该接口在自动曝光模式下使用

**函数参数：**

self.device_handle：设备句柄

params：曝光时间参数

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

### 3.1.5.3.52. scGetAutoExposureTime

**函数原型：**

```python
def scGetAutoExposureTime(self):
   params = c_int32(0)
   return self.sc_cam_lib.scGetColorAECMaxExposureTime(self.device_handle, byref(params)), params
```

**函数功能：**

获取彩色传感器在自动曝光模式下的最大曝光时间。该接口在自动曝光模式下使用

**函数参数：**

self.device_handle：设备句柄

byref(params)：返回获取的曝光时间参数

**返回值：**

[**ScReturnStatus**](#_31514-screturnstatus)：SC_OK 调用成功，其他值调用失败

**params**：返回获取的曝光时间参数

<!-- tabs:end -->
