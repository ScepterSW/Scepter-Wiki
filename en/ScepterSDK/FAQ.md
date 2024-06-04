# 5. FAQ<!-- {docsify-ignore-all} -->

## 5.1. Where is SDK log stored？

For Windows, default location: C:\Users\<user name>\AppData\Local\Scepter\Log

For Linux, default location: /home/\<user name>/.config/Scepter/Log

## 5.2. Point cloud format for SDK output

<!-- SDK 输出的点云格式为从当前帧的第一个 pixel 至最后一个 pixel 的 X,Y,Z 值，以 float 型输出，单位是 mm，说明如下： -->

The point cloud format output by SDK is the X, Y, and Z values from the first pixel to the last pixel of the current frame, output in float type, and the unit is mm. The description is as follows:

![SDK output pointcloud](<../../zh-cn/ScepterSDK/pic/SDK output pointcloud.png>)

## 5.3. ScepterSDK cannot search the camera

<!-- 搜索不到相机通常有以下几种情况：

1. 相机与主机端的接线是否良好，主机端的网卡是否可用
2. 相机与主机不在同一网段。如果相机设置为非 DHCP 模式，请确保相机的固定 IP 于主机在同一网段，如 192.168.1.X。若相机设置为 DHCP 模式，请确保相机与主机处于同 一局域网下，并且路由器/交换机具有 DHCP sever 功能
3. 软件的网络访问权限是否被限制
4. 局域网的 9007， 9008， 9009 端口是否被禁止
5. 相机的供电是否足够。如果使用非 POE 方式，请确保适配器打开并插入

如果以上检查项都确认无问题，但仍无法打开相机，请联系 FAE 处理。 -->

Following lists need to be checked if Ethernet access cameras can’t be searched.

1. Make sure good connection between the DUT and the host, and confirm if the network adapter of the host works well.
2. Make sure the DUT is under the same LAN as the host. If the DUT is set in non-DHCP mode, make sure the DUT’s fixed IP is in the same internet segment as the host, like 192.168.1.X; If the DUT is set in DHCP mode, make sure the DUT is in
   the same LAN as the host, and the router/switch has DHCP server function.
3. Make sure the software’s internet permission is not prohibited.
4. Make sure Internet UDP function is not prohibited by LAN safety policy.
5. Make sure LAN 9007, 9008, 9009 port is not prohibited.
6. Make sure power supply is correct. If not POE approach, make sure power adapter is
   plugged.

If the above check items are OK, but the camera still cannot be opened, please contact FAE.
