# 1.4. 时间同步

## 1.4.1. NTP时间同步

### 1.4.1.1. 原理与背景

3D TOF（Time of Flight）相机是一种基于光飞行时间测距原理的深度相机，通过测量红外光从发射到接收所需的时间来计算物体与相机之间的距离。</br>

NTP（Network Time Protocol）是一种用于同步网络中计算机时钟的协议，可以确保网络中的设备具有相同的时间基准。</br>
原理与背景： 在多相机系统中，为了实现精确的时间同步和数据融合，需要使用NTP功能。NTP可以使多个TOF相机在相同的时间基准下工作，从而提高数据处理的准确性和稳定性。

### 1.4.1.2. 相机使用NTP对时方法

**1)搭建网络环境：**

确保TOF相机与上位机连接到同一个局域网，并能够访问到NTP服务器。

> 1.	TOF相机通过网线连接到局域网的交换机。
> 2.	NTP服务器也通过网线连接到同一个局域网的交换机。
> 3.	所有设备在同一个局域网内，可以通过网络互相访问。

**2)配置NTP服务器：**

设置一个NTP服务器，可以是局域网内的一台计算机或者专用的NTP服务器设备。确保NTP服务器已正确配置并连接到互联网，以便获取准确的时间信息。</br>

（例如windows开始NTP Server服务）

**3)配置TOF相机NTP服务：**

<!-- tabs:start -->

#### **ScepterGUITool配置**

**Step1**: 打开ScepterGUITool连接相机后，选择进入TOF相机的Network网络设置；

**Step2**: 选择将NTP服务器的IP地址设置为第2步中配置的NTP服务器的IP地址，如下图所示：

![NTP时间同步](pic/Time%20sync%20ntp.png)

**Step3**: 设置好NTP服务器IP地址后，点击Set，设置成功。

#### **调用API结构体**

参考相机支持设置时间同步的API如下：

```cpp
ScStatus scSetTimeSyncConfig(ScDeviceHandle device, ScTimeSyncConfig params)
```

**Description：**

Get the parameters for time sync.

**Parameters：**

<span style="color: #4ec9b0; font-weight: bold">ScDeviceHandle</span> device：The handle of the device.

<span style="color: #4ec9b0; font-weight: bold">ScTimeSyncConfig</span> params : The parameters for time sync.

**Returns：**

<span style="color: #4ec9b0; font-weight: bold">ScStatus</span>：SC_OK If the function succeeded, or one of the error values defined by ::ScStatus.

参考相机支持时间同步结构体如下：

**Description：**

Time Sync parameters.

**Members：**

```cpp
typedef struct
{
    uint8_t flag;     //!< 0: disable, 1: NTP, 2: PTP, only NTP needs the ip.
    uint8_t ip[16];   //!< just for NTP.
} ScTimeSyncConfig;
```

<!-- tabs:end -->

**4)时间同步效果：**

相机设置成功后可以通过获取Time sync状态，并调取时间戳。

参考相机支持获取时间同步状态API如下：

```cpp
ScStatus scGetTimeSyncConfig(ScDeviceHandle device, ScTimeSyncConfig* pParams)
```

**Description：**

Get the parameters for time sync.

**Parameters：**

<span style="color: #4ec9b0; font-weight: bold">ScDeviceHandle</span> device：The handle of the device.

<span style="color: #4ec9b0; font-weight: bold">ScTimeSyncConfig</span>* pParams : The parameters for time sync.

**Returns：**

<span style="color: #4ec9b0; font-weight: bold">ScStatus</span>：SC_OK If the function succeeded, or one of the error values defined by ::ScStatus.

若NTP Server adress：192.168.1.100，下面举出一个Demo例程：

```cpp
	//Get ScTimeSyncConfig timeparams
	ScTimeSyncConfig timeparams = { };
	status = scGetTimeSyncConfig(deviceHandle, &timeparams);
	if (status != ScStatus::SC_OK)
	{
		cout << "scGetTimeSyncConfig failed status:" << status << endl;
		return -1;
	}
	 cout << "Get TimeSyncConfig flag: " << timeparams.flag << endl;
	 cout << "Get TimeSyncConfig ip: " << timeparams.ip << endl;
	//Cout deviceTimestamp
	ScFrame depthFrame = {};
	status = scGetFrame(deviceHandle, SC_DEPTH_FRAME, &depthFrame);
	cout << &depthFrame.deviceTimestamp << endl;
```

输出结果：
```console
Get TimeSyncConfig flag:1
Get TimeSyncConfig ip:192.168.1.100
000000006673C1A8
```

再将16进制时间戳转化为时间：
```time
2024-06-20 13:44:08
```

再与NTP Server时间进行比较，从而得出差值。

## 1.4.2 PTP时间同步




