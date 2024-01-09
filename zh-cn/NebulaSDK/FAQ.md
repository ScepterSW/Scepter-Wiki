# 8. FAQ<!-- {docsify-ignore-all} -->

## 8.1. SDK 日志存放位置

Windows 上默认日志路径：C:\Users\\\<user name>\AppData\Local\Vzense\Log

Linux 上默认日志路径： /home/\<user name>/.config/Vzense/Log

## 8.2. SDK 输出的点云格式

SDK 输出的点云格式为从当前帧的第一个 pixel 至最后一个 pixel 的 X,Y,Z 值，以 float 型输出，单位是 mm，说明如下：

![SDK output pointcloud](<pic/SDK output pointcloud.png>)

## 8.3. 无法打开相机的排查步骤

搜索不到相机通常有以下几种情况：

1. 相机与主机端的接线是否良好，主机端的网卡是否可用
2. 相机与主机不在同一网段。如果相机设置为非 DHCP 模式，请确保相机的固定 IP 于主机在同一网段，如 192.168.1.X。若相机设置为 DHCP 模式，请确保相机与主机处于同 一局域网下，并且路由器/交换机具有 DHCP sever 功能
3. 软件的网络访问权限是否被限制
4. 局域网的 9007， 9008， 9009 端口是否被禁止
5. 相机的供电是否足够。如果使用非 POE 方式，请确保适配器打开并插入

如果以上检查项都确认无问题，但仍无法打开相机，请联系 FAE 处理。
