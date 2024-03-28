# 快速开始

<!-- tabs:start -->

#### **Windows**

1. 通过电源线或多功能线给相机提供 12~24V 电源（典型值：12V 3A），

   **NYX660/VENO87** 支持 PoE+供电模式，推荐使用以下 PoE+供电器：

   | 供应商  | 型号        |
   | :------ | :---------- |
   | H3C     | EWPAM2NPoE+ |
   | TP LINK | TL-PoE+170S |

2. 通过以太网线/航插网线将相机连接至主机。

   ![DeviceConnection](pic/DeviceConnection.png)
   _硬件模组安装示意图_

3. 设置主机 IP 地址与相机在同一网段，设备默认 IP 为 **192.168.1.101**。

   设置 Windows 端的**本地连接**，子网掩码设为 255.255.255.0，

   IP 地址设为同一网段（如 192.168.1.100）。

   <div class="center">

   ![固定地址](pic/WindowsStaticAddress.png)

   </div>

   **注意：**

   ① 主机端使用的网卡、路由器、交换机都要满足**千兆**要求。

   ② 在首次运行 ScepterGUITool 时，要为程序设置通过系统防火墙的权限，如下图所示。

   <div class="center">

   ![防火墙配置](pic/WindowsFirewallSetting.png)

   </div>

   ③ 当使用多个网卡时，需要设置不同的 IP 网段。当多个网卡被配置为相同的 IP 地址段时，这会导致网络冲突和连接问题。在这种情况下，如果主机与相机之间的连接中断，由于 IP 地址冲突，其他设备也可能无法与主机建立或维持连接。为了避免这种情况，每个网卡应该被分配不同的 IP 网段，确保网络中的每一台设备都能稳定地通信。

4. 用户可通过下述链接下载 **ScepterGUITool**：

   <https://github.com/ScepterSW/ScepterGUITool>

   镜像加速地址：<https://gitee.com/ScepterSW/ScepterGUITool>

   ScepterGUITool 包含 ScepterGUITool 可执行文件，用户手册文档及相关动态链接库。

   ![目录结构](pic/WindowsContents.png)

5. 双击 ScepterGUITool 可执行文件，运行 ScepterGUITool，按照以下步骤连接设备：

   ① 搜索设备

   ② 选中设备的 SN

   ③ 点击 Open 打开设备，或者双击设备 SN 打开设备

   ![设备连接](pic/ConnectDevice.png)

6. 按照 ScepterGUITool 使用指南，开始探索相机。

#### **Ubuntu**

1. 通过电源线或多功能线给相机提供 12~24V 电源（典型值：12V 3A），

   **NYX660/VENO87** 支持 PoE+供电模式，推荐使用以下 PoE+供电器：

   | 供应商  | 型号        |
   | :------ | :---------- |
   | H3C     | EWPAM2NPoE+ |
   | TP LINK | TL-PoE+170S |

2. 通过以太网线/航插网线将相机连接至主机。

   ![DeviceConnection](pic/DeviceConnection.png)
   _硬件模组安装示意图_

3. 设置 Linux 端的**本地连接**，子网掩码设为 255.255.255.0，IP 地址设为同一网段（如 192.168.1.100）。

   <div class="center">

   ![LinuxEditConnections](pic/LinuxEditConnections.png)

   </div>

   <div class="center">

   ![LinuxEdit](pic/LinuxEdit.png)

   </div>

   <div class="center">

   ![固定地址](pic/LinuxStaticAddress.png)

   </div>

   **注意：**

   ① 主机端使用的网卡、路由器、交换机都要满足**千兆**要求。

   ② 当使用多个网卡时，需要设置不同的 IP 网段。当多个网卡被配置为相同的 IP 地址段时，这会导致网络冲突和连接问题。在这种情况下，如果主机与相机之间的连接中断，由于 IP 地址冲突，其他设备也可能无法与主机建立或维持连接。为了避免这种情况，每个网卡应该被分配不同的 IP 网段，确保网络中的每一台设备都能稳定地通信。

4. 用户可通过下述链接下载 **ScepterGUITool**，

   ScepterGUITool 支持 Ubuntu18.04(x86/x64) 及以上操作系统：

   <https://github.com/ScepterSW/ScepterGUITool>

   镜像加速地址：<https://gitee.com/ScepterSW/ScepterGUITool>

   ScepterGUITool 包含 ScepterGUITool 可执行文件，用户手册文档及相关动态链接库。

   ![目录结构](pic/LinuxContents.png)

5. 双击 ScepterGUITool 可执行文件，运行 ScepterGUITool，按照以下步骤连接设备：

   ① 搜索设备

   ② 选中设备的 SN

   ③ 点击 Open 打开设备，或者双击设备 SN 打开设备

   ![设备连接](pic/ConnectDevice.png)

6. 按照 ScepterGUITool 使用指南，开始探索相机。

#### **ARM-Linux**

1. 通过电源线或多功能线给相机提供 12~24V 电源（典型值：12V 3A），

   **NYX660/VENO87** 支持 PoE+供电模式，推荐使用以下 PoE+供电器：

   | 供应商  | 型号        |
   | :------ | :---------- |
   | H3C     | EWPAM2NPoE+ |
   | TP LINK | TL-PoE+170S |

2. 通过以太网线/航插网线将相机连接至主机。

   ![DeviceConnection](pic/DeviceConnection.png)
   _硬件模组安装示意图_

3. 设置 ARM-Linux 端的**本地连接**，子网掩码设为 255.255.255.0，IP 地址设为同一网段（如 192.168.1.100）。

   **注意：**

   ① 主机端使用的网卡、路由器、交换机都要满足**千兆**要求。

   ② 当使用多个网卡时，需要设置不同的 IP 网段。当多个网卡被配置为相同的 IP 地址段时，这会导致网络冲突和连接问题。在这种情况下，如果主机与相机之间的连接中断，由于 IP 地址冲突，其他设备也可能无法与主机建立或维持连接。为了避免这种情况，每个网卡应该被分配不同的 IP 网段，确保网络中的每一台设备都能稳定地通信。

4. 用户可通过下述链接下载 **ScepterSDK**，

   <https://github.com/ScepterSW/ScepterSDK>

   镜像加速地址：<https://gitee.com/ScepterSW/ScepterSDK>

   ScepterSDK 包含一系列友好的 API ，简单的应用示例程序，用户手册文档及相关动态链接库。

   ![目录结构]()

5. 进入 AArch64/PrecompiledSamples 文件夹，使用终端打开对应相机的预编译好的程序：

   ![设备连接]()

6. 按照 ScepterSDK 使用指南，开始探索相机。

<!-- tabs:end -->

<style>
.center
{
  width: auto;
  display: table;
  margin-left: auto;
  margin-right: auto;
}
</style>
