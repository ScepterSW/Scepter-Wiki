# 点云格式说明

1.SDK 输出的点云格式为从当前帧的第一个 pixel 至最后一个 pixel 的 X,Y,Z 值，以 float 型输出，单位是 mm，说明如下：

![SDK output pointcloud](<pic/SDK output pointcloud.png>)

2.GUITool 保存的.txt 格式点云图，从上到下行依次为 pixel 0 至最后一个 pixel，每一 行的数值依次为该 pixel 的 X,Y,Z 值，说明如下：

![.txt point cloud file](<pic/txt point cloud file.png>)​

3.可通过 CloudCompare 工具来查看保存下来的点云图，下载链接为：<http://www.cloudcompare.org/release/index.html#CloudCompare>
