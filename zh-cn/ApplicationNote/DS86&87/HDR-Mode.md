# 2.3. HDR 模式

ToF(Time-of-Flight)感知技术作为三维视觉成像领域主流技术之一，发展迅猛，伴随着半导体元器件尺寸的不断缩小，结构紧凑、极具性价比优势的 TOF 深度相机得到了越来越多的行业关注，在工业和消费电子领域针对整个场景的多点 3D 视觉、3D 建模辅助、3D 深度感知等场景，应用需求日益增加。

ToF 深度相机是一种主动成像的方式，即相机系统向目标发射激光，通过接收端传感器感知到目标反射光的时间，从而计算出目标与相机之间的距离。TOF 深度相机技术是通过一次性成像来提供完整场景深度图，无扫描器件，成像速度快，计算负荷低，不论对于移动中的物体，还是静态的物体，不论在黑暗环境中，还是在室外光照较强烈的环境中，不论对于低反射率还是高反射率的物体，都有机会获取到较为理想的深度数据。

鉴于上述优点，ToF 相机已经越来越多地应用于 3D 检测与识别、AGV 避障、机械手抓取、体积测量等工业场景中。

<div class="center">

![TOF Camera Principles](<HDR-Mode-asserts/01.png>)

</div>

本文重点介绍在复杂环境中，当同时存在高反光率物体如金属件与低反光率如黑色表面物体时，如何通过技术手段提升 ToF 相机的检测精度。

首先，从 ToF 相机的检测原理来理解这个问题，当采用固定曝光时间模式时，相机在同时拍摄高反射率与低反射率物体时，较难将曝光时间调到一个均衡的位置，可同时准确地捕捉到高反射率与低反射率物体的深度图像；当我们增加曝光时间时，利于黑色物体的识别，但近距离区域容易出现过曝的现象；而降低曝光时间时，对于低反射率物体的识别又会存在点云缺失的现象。

为了解决这个问题，维感科技在 ToF 相机曝光时间方面增加了 HDR 高动态范围模式：即通过设置多个不同曝光时间的方式，将采集到的多个图像合成到一帧中，完成对整个复杂场景的成像。

在针对距离较近易过曝的区域与高反射率物体时，利用短曝光时间进行成像；在针对低反射率的物体时，利用长曝光时间进行成像，最终将不同曝光时间下取得的图像合成到一帧中，从而获得更为精确的深度图像，减少距离远近与物体反射率差异对 ToF 相机深度检测数据的影响。

<div class="center">

![HDR mode measurement judgment](<HDR-Mode-asserts/02.png>)

</div>

下面将通过两个实例解释 ToF 相机如何通过开启 HDR 功能来改善对复杂场景中同时存在高低反射率物体时的拍摄效果。

**成像实例：**

实例一：拍摄下述杂乱物体

<div class="center">

![Cutter Objects](<HDR-Mode-asserts/03.png>)

</div>

**未开启 HDR 模式**

单一低曝光时间的情况下，低反射率的黑色胶皮线点云数据缺失；

<div class="center">

![HDR off ExposureTime58μs](<HDR-Mode-asserts/04.png>)

</div>

单一高曝光时间的情况下，高反射率的泡沫包裹和白色纸箱点云数据缺失。

<div class="center">

![HDR off ExposureTime1000μs](<HDR-Mode-asserts/05.png>)

</div>

**开启 HDR 模式后**，ToF 相机首先使用高曝光时间对低反射率的物体进行成像，对于高曝光时间下过曝的区域，使用低曝光时间进行成像，最终将不同曝光时间下取得的图像合成到一帧中，即可得到 HDR 模式开启下的图像，可以看到点云数据缺失的问题得到了明显改善。

<div class="center">

![HDR on](<HDR-Mode-asserts/06.png>)

</div>

实例二：拍摄轿车车轮

<div class="center">

![Car Wheel](<HDR-Mode-asserts/07.png>)

</div>

**未开启 HDR 模式**

单一低曝光时间的情况下，低反射率的黑色轮胎点云数据缺失；

<div class="center">

![ Car HDR off ExposureTime58μs ](<HDR-Mode-asserts/08.png>)

</div>

单一高曝光时间的情况下，高反射率的金属轮毂出现了过曝现象，点云数据缺失。

<div class="center">

![Car HDR off ExposureTime1000μs](<HDR-Mode-asserts/09.png>)

</div>

开启 HDR 模式后，点云数据缺失的问题得到了明显改善，无论低反射率的黑色轮胎，还是高反射率的金属轮毂的点云数据都是较为完整准确的。

<div class="center">

![Car HDR on](<HDR-Mode-asserts/10.png>)

</div>

ToF 相机的 HDR 模式，在很大程度上拓展了其在工业领域与服务类机器人方面的应用。

<style>
.center
{
  width: auto;
  display: table;
  margin-left: auto;
  margin-right: auto;
}
</style>
