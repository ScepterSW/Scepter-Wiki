# 2.3. HDR Mode

ToF (Time-of-Flight) perception technology, as one of the mainstream technologies in the field of three-dimensional visual imaging, has developed rapidly. With the continuous reduction of semiconductor components, ToF depth camera with compact structure and high cost-effective advantage has become more and more. Industry attention, in the industry and consumer electronics fields, multi -point 3D vision, 3D modeling assistance, 3D depth perception of 3D modeling, 3D depth perception of the entire scene, have increasing application demand.

ToF depth camera is an active imaging method, that is, the camera system laser laser to the target, and the time of the target reflection light is perceived by the receiving end sensor, so as to calculate the distance between the target and the camera. ToF depth camera technology provides a complete scene depth map through disposable imaging. There is no scanning device, the imaging speed is fast, and the calculation load is low. In a strong environment, no matter for low -reflectance or high reflectivity objects, there is a chance to obtain more ideal depth data.

In view of the above advantages, ToF camera has increasingly applied in industrial scenarios such as 3D detection and recognition, AGV obstacle avoidance, robotic grabbing, volume measurement, and other industrial scenarios.

<div class="center">

![TOF Camera Principles](<../../../zh-cn/ApplicationNote/DS86&87/HDR-Mode-asserts/01.png>)

</div>

This article focuses on how to improve the detection accuracy of the ToF camera through technical means when high reflective objects such as metal parts and low reflective rates such as black surface objects at the same time.

First of all, understand this problem from the detection principle of the ToF camera. When the fixed exposure time mode is adopted, the camera is more difficult to adjust the exposure time to a balanced position when shooting high reflectivity and low reflectivity objects at the same time. The depth image of high-reflectance and low reflectivity objects is captured by the ground; when we increase the exposure time, it is conducive to the identification of black objects, but the phenomenon of over-exposure is prone to the close-range area; and when the exposure time is reduced, the low reflectivity object is for low reflectivity objects. There will be some pointcloud lack of recognition.

To solve this problem, Vzense added HDR mode to the ToF camera: by setting multiple different exposure times, multiple images captured are combined into one frame to complete the imaging of the whole complex scene.

Use short exposure time to shoot area which is closer and easy to over-exposure or high reflectivity objects. Use long exposure time to shoot low-reflectance objects. Finally, the images obtained in different exposure time are synthesized into a frame,so as to obtain a more accurate depth image,reduce the effect of difference distance and reflectivite on the deep detection of the ToF camera.

<div class="center">

![HDR mode measurement judgment](<HDR-Mode-asserts/01.png>)

</div>

The following will explain how the ToF camera will be explained through the HDR function to improve the shooting effect when there are high and low reflectivity objects in complex scenarios.

**Example：**

Example1：Following clutter objects

<div class="center">

![Cutter Objects](<../../../zh-cn/ApplicationNote/DS86&87/HDR-Mode-asserts/03.png>)

</div>

**HDR off**

In the case of a single low exposure time, the low-reflectance black rubber line point cloud data is missing.

<div class="center">

![HDR off ExposureTime58μs](<../../../zh-cn/ApplicationNote/DS86&87/HDR-Mode-asserts/04.png>)

</div>

In the case of a single high exposure time, the high-reflectance foam wrap and the white carton point cloud data is missing.

<div class="center">

![HDR off ExposureTime1000μs](<../../../zh-cn/ApplicationNote/DS86&87/HDR-Mode-asserts/05.png>)

</div>

After turning on the **HDR mode**, ToF camera first uses a high exposure time to image the low-reflectance objects. For the area where high exposure time is over-exposed, the low exposure time is used for imaging. Finally In the frame, you can get the image with HDR mode. The problem of missing point cloud data has been significantly improved.

<div class="center">

![HDR on](<../../../zh-cn/ApplicationNote/DS86&87/HDR-Mode-asserts/06.png>)

</div>

Example2：Car wheel

<div class="center">

![Car Wheel](<../../../zh-cn/ApplicationNote/DS86&87/HDR-Mode-asserts/07.png>)

</div>

**HDR off**

In the case of a single low exposure time, the black tire point cloud data data of low reflectivity is missing.

<div class="center">

![ Car HDR off ExposureTime58μs ](<../../../zh-cn/ApplicationNote/DS86&87/HDR-Mode-asserts/08.png>)

</div>

In the case of a single high exposure time, a high-reflectance metal wheel has a overexposure phenomenon, and the point cloud data is missing.

<div class="center">

![Car HDR off ExposureTime1000μs](<../../../zh-cn/ApplicationNote/DS86&87/HDR-Mode-asserts/09.png>)

</div>

After turning on the **HDR mode**, the problem of lack of point cloud data has been significantly improved. Black tires with low reflectivity or metal wheels with high reflectivity are more complete and accurate.

<div class="center">

![Car HDR on](<../../../zh-cn/ApplicationNote/DS86&87/HDR-Mode-asserts/10.png>)

</div>

HDR mode of the ToF camera has largely expanded its application in the industrial field and service robots.

<style>
.center
{
  width: auto;
  display: table;
  margin-left: auto;
  margin-right: auto;
}
</style>
