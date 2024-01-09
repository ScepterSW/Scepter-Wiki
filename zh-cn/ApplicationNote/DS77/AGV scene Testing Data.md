# 2.4. 场景测试数据

## 2.4.1. 介绍

3D ToF 技术应用于各类 AGV/AMR 及低速无人驾驶领域。多传感器融合不仅可以为无人驾驶提供全方位避障解决方案，提升系统安全系数，还可以更好地感知环境，识别目标物体，并自动规划行车路线。Vzense 3D ToF 相机具有性价比高，实时性好，对系统算力要求低，且适合运动中的场景捕捉等特点。

应用于无人叉车托盘自动识别，Vzense 3D ToF 相机可以通过采集托盘图像，结合相应图像处理算法，对叉车货物托盘进行识别，并得到其位置与姿态坐标，智能调整进叉方向，从而实现无人化智能托盘搬运，解决无人叉车对接托盘位置偏移角度较大的问题。

应用于 AGV 避障，Vzense 3D ToF 相机基于其面阵探测的原理，为移动机器人及低速无人驾驶车提供近距离（<6m）大角度的避障方案。

## 2.4.2. 测试条件

**目标物体**：黑色托盘、蓝色托盘、木质托盘、购物车、覆膜盒子、黑色圆柱体（参考图 1）。

**相机位置**：相机用高度 215mm 的支架固定，放置在地面上（参考图 2）。

**相机设置**：拍摄黑色物体设置 4ms 的曝光时间，低置信度阈值（参考图 3），相机预热 20 分钟。

拍摄其他物体采用默认设置（参考图 4），相机预热 20 分钟。

**成像环境**：22°C 室温，测试期间室内光线为 200Lux。

**拍摄黑色物体设置**：DS 系列相机默认曝光时间为 1ms，在 NebulaGUITool 中可以通过调低 Frame rate 的方式，来增加曝光时间。设置 Frame rate 为 5 帧，可调整 Exposure Time 为 4ms。

**低置信度阈值**：黑色物体的反射率较低，会导致信噪比过低而无法测量物体距离，为改善此情况，拍摄黑色物体时通常将 ConfidenceFilter 降低为 2 或 5。

|                                                                                     |
| :---------------------------------------------------------------------------------: |
|                              ![Target](pic/Target.png)                              |
|                                   图 1：目标物体                                    |
|                 ![Camera Positioning](<pic/Camera Positioning.png>)                 |
|                                   图 2：相机位置                                    |
| ![Setting for Shooting Black Objects](<pic/Setting for Shooting Black Objects.png>) |
|                               图 3：拍摄黑色物体设置                                |
|                    ![Default Setting](<pic/Default Setting.png>)                    |
|                                   图 4：默认设置                                    |

## 2.4.3. 测试数据

**保存的数据和图像**：Depth, IR, PointCloud, RGB

**环境光**：室内光，约 200lux

**相机位置**：相机距离地面 215mm

**距离**：1m，2m，3m

### 2.4.3.1. 黑色托盘

![Black pallet](<pic/Black pallet.png>)

查看在线点云：

DS77C_1m away Black pallet：<https://skfb.ly/oCEZM>​

DS77C_2m away Black pallet：<https://skfb.ly/oCEZQ>​

DS77C_3m away Black pallet：<https://skfb.ly/oCEZR>​

### 2.4.3.2. 蓝色托盘

![Blue pallet](<pic/Blue pallet.png>)

查看在线点云：

DS77C_1m away Blue pallet：<https://skfb.ly/oCFny>​

DS77C_2m away Blue pallet：<https://skfb.ly/oCFnA>​

DS77C_3m away Blue pallet：<https://skfb.ly/oCFnE>​

### 2.4.3.3. 木质托盘

![Wooden pallet](<pic/Wooden pallet.png>)

查看在线点云：

DS77C_1m away Wooden pallet：<https://skfb.ly/oCMTu>​

DS77C_2m away Wooden pallet：<https://skfb.ly/oCMTC>​

DS77C_3m away Wooden pallet：<https://skfb.ly/oCMTL>​

### 2.4.3.4. 购物车

![Shopping cart](<pic/Shopping cart.png>)

查看在线点云：

DS77C_1m away Shopping cart：<https://skfb.ly/oCFnQ>​

DS77C_2m away Shopping cart：<https://skfb.ly/oCFor>​

DS77C_3m away Shopping cart：<https://skfb.ly/oCFon>​

### 2.4.3.5. 覆膜盒子

![Box covered with film](<pic/Box covered with film.png>)

查看在线点云：

DS77C_1m away Box covered with film：<https://skfb.ly/oCFoW>​

DS77C_2m away Box covered with film：<https://skfb.ly/oCFsP>​

DS77C_3m away Box covered with film：<https://skfb.ly/oCFt6>​

### 2.4.3.6. 黑色圆柱体

![Black cylinder](<pic/Black cylinder.png>)

查看在线点云：

DS77C_1m away Black cylinder：<https://skfb.ly/oCFtt>​

DS77C_2m away Black cylinder：<https://skfb.ly/oCFtx>​

DS77C_3m away Black cylinder：<https://skfb.ly/oCFtA>
