# 1.2. 多机共存

## 1.2.1. 原理与背景

Vzense 3D 深度相机采用基于 ToF（Time-of-Flight）飞行时间的方式进行距离测量。在工作中，相机会发出红外光，光遇到物体后反射回传感器，相机通过计算光发射与返回的时间差计算物体的距离。

<div class="center">

![Principle and Background](<pic/Principle and Background.png>)

</div>

因为测量过程中需要主动发送红外光，所以多台相机在同一场景下（FOV 有交叠）工作时，可能发生相互干扰的情况。多相机的干扰导致深度测量产生大量误差，深度质量严重下降，这极大限制了 ToF 相机的应用。基于以上问题我们提供了多机共存的方法。

## 1.2.2. 相机工作时序

相机每个工作周期都会进行红外光发射与采集，并计算每个像素点的距离值。每秒钟可进行测量的次数，称之为帧率。

DS86\&DS87 系列相机的典型帧率为 15fps，即每秒可产生 15 帧的深度图像信息，所以其工作周期时间为 1s / 25 = 66.67ms，则每个工作周期的时间即为 66.67 毫秒。

细分每个工作周期，又可以分为曝光（激光发射与采集）、传输两个阶段，如下图：

![exposure and transmission](<pic/exposure and transmission.png>)

当多台相机同时工作时，假如曝光阶段正好发生重叠，A 相机接收到了 B 相机发射出来的激光，就会发生相互干扰的现象。

## 1.2.3. 从触发模式

我司生产的 ToF 产品支持从触发模式。在该模式下，相机会等待收到触发信号，再开始一帧的曝光和传输。每一次信号仅触发一次曝光和传输。

您可以通过 GUI 工具或 API 函数切换相机到从触发模式，具体可以查看 GUI 工具手册和 API 文档。

### 1.2.3.1. 硬件触发：

您可以查看相关产品的产品规格书，在“产品接口”部分找到“硬件触发功能”对应的内容，以及相关硬件接口来实现从触发模式。

### 1.2.3.2. 软件触发：

可以通过调用 API 函数完成对相机的触发，具体可以查看 Gitee 或 GitHub 上对应平台 Samples 文件夹下的例程 DeviceSWTriggerMode。

SDK 链接：

国内：<https://gitee.com/Vzense>​

海外：<https://github.com/Vzense>​

## 1.2.4. 多机共存方式与用法

基于 ToF 的原理和 Vzense 提供的从触发模式，Vzense DS 系列多机共存可通过协同控制方式来实现。

协同控制方式是将多台相机全部设置为 Trigger 模式，由主控平台分别控制不同相机的曝光开始时间，保证不同相机之间不会相互干扰。相机进入 Trigger 模式后，当接收到一次触发信号后，只会工作一个工作周期，所以可以根据需求，灵活的控制不同相机的出图时间以及帧率。但需要注意，此方式需要平衡帧率与相机数量。

![Multi-Cameras Coexist](<pic/Multi-Cameras Coexist.png>)

**适应场景**：2 台以上相机同时工作，对相机的工作帧率没有过高的要求。

**使用方法：**

**1) 硬件触发：**

根据所选相机的型号，参考规格书找到 Ext_Trigger 信号引脚。将相应的触发信号分别接到 A,B,C 相机的触发引脚。

![Hardware trigger](<pic/Hardware trigger.png>)

**2) 软件触发：**

将 A,B,C 相机全部设置为 slave 模式。等待触发信号的触发。

VzReturnStatus VZ_SetWorkMode(VzDeviceHandle device, VzWorkMode mode)

由于相机不同模式下，曝光时间不同，建议相邻相机的触发信号间隔大于等于一个工作周期。例如，以 25fps 为例，A 相机触发信号发出后，B 相机的触发信号要延时 40ms 以上。

<style>
.center
{
  width: auto;
  display: table;
  margin-left: auto;
  margin-right: auto;
}
</style>
