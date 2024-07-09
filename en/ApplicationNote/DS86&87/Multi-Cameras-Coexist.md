# 2.4. Multi-Cameras Coexist

## 2.4.1. Principle and Background

3D depth camera is based on ToF (Time-of-Flight) for distance measurement. In operation, the camera emits infrared light, which is reflected to the sensor when it encounters an object, and the camera calculates the distance to the object by calculating the time difference between the emission and return of the light.

<div class="center">

![Principle and Background](<../../../zh-cn/ApplicationNote/DS86&87/Multi-Cameras-Coexist-asserts/01.png>)

</div>

Because the measurement process requires active infrared light transmission, mutual interference may occur when multiple cameras work in the same scene (with overlapping FOVs). The interference of multiple cameras leads to many errors in depth measurement and serious degradation in depth quality, which greatly limits the application of ToF cameras. Based on the above problems we provide a Multi-Cameras Coexist method.

## 2.4.2. Camera operation timing

Each working cycle of the camera will be transmitted and collected in infrared light, and the distance value of each pixel point is calculated. The number of measurements per second is called frame rate.

The typical frame rate of DS86&87 series cameras is 15fps, that is the depth image information of 15 frames can be generated per second, so the working cycle time is 1s / 15 = 40ms, and the time of each working cycle is 66.67 milliseconds.

Segmentation of each working cycle can be divided into two stages: exposure (laser launch and collection), transmission, as shown below:

![exposure and transmission](<../../../zh-cn/ApplicationNote/DS86&87/Multi-Cameras-Coexist-asserts/02.png>)
When multiple cameras work at the same time, if the exposure phase overlaps, the A camera receives the laser emitted by the B camera, which will interfere with each other.

## 2.4.3. Slave Trigger Mode

The ToF product produced by us supports the trigger mode. In this mode, the camera will wait for the trigger signal, and then start a frame of exposure and transmission. Each signal only triggers one exposure and transmission.

The camera can be switched to the trigger mode through the GUI tool or API function, and it can be viewed in the GUI Tool Manual and API documents in detail.

### 2.4.3.1. Hardware trigger:

You can view the ToF Camera Specification, find corresponding content to " Hardware Trigger Function" in " Interface with Host" section, and related hardware interfaces to achieve a trigger mode.

### 2.4.3.2. Software trigger:

You can complete the trigger by calling the API function. For details, you can view the sample program DeviceSWTriggerMode under the corresponding platform Samples folder on the Gitee or GitHub.

SDK link:

https://github.com/ScepterSW/ScepterSDK

or

https://gitee.com/ScepterSW/ScepterSDK

## 2.4.4. Multi-Cameras Coexist

Based on the principle of ToF and the trigger mode, Multi-Cameras Coexist can be implemented by Center Controller Synchronization.

1. Set multiple cameras as slave trigger mode, please find the operation steps in the user manual of the camera.

2. Use a center controller to generate the trigger signal for each camera. Make sure the timing of each trigger signal is timing divided.

![Multi-Cameras Coexist](<../../../zh-cn/ApplicationNote/DS86&87/Multi-Cameras-Coexist-asserts/03.png>)

**Adaptation scene**: Two or more cameras work at the same time, and there are no requirements for the working frame rate of the camera.

**Usage:**

**1) Hardware trigger：**

Please find the Ext_Trigger signal, and connect the trigger signal from the center controller to the cameras.

![Hardware trigger](<../../../zh-cn/ApplicationNote/DS86&87/Multi-Cameras-Coexist-asserts/04.png>)

**2) Software trigger：**

Set all A, B, C camera to Slave mode. Waiting for triggering signals.

ScStatus scSetWorkMode(ScDeviceHandle device, ScWorkMode mode)

Due to the different exposure time of the camera in different modes, it is recommended that the trigger signal interval between adjacent cameras is greater than equal to a working cycle. For example, taking 15FPS as an example, after the A camera triggered the signal, the trigger signal of the B camera should be delayed above 66.7ms.

<style>
.center
{
  width: auto;
  display: table;
  margin-left: auto;
  margin-right: auto;
}
</style>
