## 1. 设备连接<!-- {docsify-ignore-all} -->

1. 将相机安装在一个合适的固定装置中，例如相机支架。

![DeviceConnection](pic/DeviceConnection.png)

2. 通过多功能线为相机提供 12~24V 电源（典型值：12V 3A）。部分型号可选用 PoE+供电模式，具体请参考产品规格书。

3. 此时设备处于以太网广播无连接建立的状态，侧面用于显示相机的状态的 LED 指示灯会呈**蓝色**并且反复闪烁。

![BlueLed1](pic/BlueLed1.png)

4. 设置主机 IP 地址与相机在同一网段，设备默认 IP 为 **192.168.1.101**。

<!-- tabs:start -->

#### **Windows**

设置 Windows 端的本地连接，子网掩码设为 255.255.255.0，IP 地址设为同一网段（如 192.168.1.100）。

   <div class="center">

![固定地址](pic/WindowsStaticAddress.png)

   </div>

#### **Ubuntu**

设置 Linux 端的本地连接，子网掩码设为 255.255.255.0，IP 地址设为同一网段（如 192.168.1.100）。

   <div class="center">

![LinuxEditConnections](pic/LinuxEditConnections.png)

   </div>

   <div class="center">

![LinuxEdit](pic/LinuxEdit.png)

   </div>

   <div class="center">

![固定地址](pic/LinuxStaticAddress.png)

   </div>

#### **AArch64**

设置 ARM-Linux 端的**本地连接**，子网掩码设为 255.255.255.0，IP 地址设为同一网段（如 192.168.1.100）。可选用 numtui 进行设置。

```consle
sudo numtui
```

   <div class="center">

![固定地址](pic/ARMLinuxStaticAddress.png)

   </div>

<!-- tabs:end -->

> ① 主机端使用的网卡、路由器、交换机都要满足**千兆**要求。
>
> ② 当使用多个网卡时，需要设置不同的 IP 网段。当多个网卡被配置为相同的 IP 地址段时，这会导致网络冲突和连接问题。在这种情况下，如果主机与相机之间的连接中断，由于 IP 地址冲突，其他设备也可能无法与主机建立或维持连接。为了避免这种情况，每个网卡应该被分配不同的 IP 网段，确保网络中的每一台设备都能稳定地通信。

## 2. 打开设备

1.  Windows 端 和 Ubuntu18.04/20.04/22/04 端用户可下载 **ScepterGUITool**探索相机，

    Ubuntu16.04 端无图形化工具，AArch64 端常用 headless 模式，用户可下载 **ScepterSDK**探索相机：

    <!-- tabs:start -->

    #### **ScepterGUITool**

    ScepterGUITool 下载链接：

    <https://github.com/ScepterSW/ScepterGUITool>

    或

    <https://gitee.com/ScepterSW/ScepterGUITool>

    下面介绍两种下载方式：

    <!-- tabs:start -->

    #### **方式一**

    可以通过 git clone 到本地，方法如下：

    Step1：打开下载链接，点击 Code，复制链接；

    ```
    git clone https://github.com/ScepterSW/ScepterGUITool
    ```

    ![git clone http](<pic/git clone http.png>)

    Step2：打开终端，输入复制代码回车，等待下载完成。

    ![git clone GUITool.png](<pic/git clone GUITool.png>)

    #### **方式二**

    打开下载链接，点击 Code，再点击 Download ZIP，即可将 ScepterGUITool 工具压缩包下载到本地。

    如需在 Ubuntu 系统下使用，请确保下载后的压缩包是在 Ubuntu 系统下解压，请勿在 Windows 系统解压后复制使用。

    ![GitHub GUITool](<pic/GitHub GUITool.png>)

    <!-- tabs:end -->

    #### **ScepterSDK**

    ScepterSDK 下载链接：

    <https://github.com/ScepterSW/ScepterSDK>

    或

    <https://gitee.com/ScepterSW/ScepterSDK>

    下面介绍两种下载方式：

    <!-- tabs:start -->

    #### **方式一**

    可以通过 git clone 到本地，方法如下：

    Step1：打开下载链接，点击 Code，复制链接；

    ```
    git clone https://github.com/ScepterSW/ScepterSDK
    ```

    ![git clone SDK http](<pic/git clone SDK http.png>)

    Step2：打开终端，输入复制代码回车，等待下载完成。

    ![git clone ScepterSDK](<pic/git clone ScepterSDK.png>)

    #### **方式二**

    打开下载链接，点击 Code，再点击 Download ZIP，即可将 ScepterSDK 压缩包下载到本地。

    如需在 Ubuntu 系统下使用，请确保下载后的压缩包是在 Ubuntu 系统下解压，请勿在 Windows 系统解压后复制使用。

    ![GitHub ScepterSDK](<pic/GitHub ScepterSDK.png>)

    <!-- tabs:end -->

    <!-- tabs:end -->

2.  ScepterGUITool 包含 ScepterGUITool 可执行文件及相关动态链接库。

    ScepterSDK 包含一系列友好的 API ，应用示例程序及相关动态链接库。

   <!-- tabs:start -->

    #### **ScepterGUITool**

    <!-- tabs:start -->

    #### **Windows**

      ![目录结构](pic/WindowsContents.png)

      > 在首次运行 ScepterGUITool 时，要为程序设置通过系统防火墙的权限，如下图所示。
      >
      >  <div class="center">
      >
      > ![防火墙配置](pic/WindowsFirewallSetting.png)
      >
      >  </div>

    #### **Ubuntu**

      ![目录结构](pic/LinuxContents.png)

   <!-- tabs:end -->

      双击 ScepterGUITool 可执行文件，运行 ScepterGUITool，按照以下步骤连接设备：

      ① 搜索设备

      ② 选中设备的 SN

      ③ 点击 Open 打开设备，或者双击设备 SN 打开设备

      ![设备连接](pic/DeviceList.png)

      ③ 打开成功后，图像在右侧正常显现。

      ![图像显现](pic/DisplayArea.png)

      ④ 此时设备处于以太网广播连接建立的状态，侧面用于显示相机的状态的 LED 指示灯会呈**蓝色**并且常亮。

      ![BlueLed2](pic/BlueLed2.png)

      您可以参考[Scepter 图形化工具介绍](/zh-cn/ScepterGUITool/Overview.md)了解相机的详细功能，开始探索相机。

    #### **ScepterSDK**

    <!-- tabs:start -->

    #### **AArch64**

      ![目录结构](pic/ARMLinuxContents.png)

      进入 AArch64/PrecompiledSamples 文件夹，使用终端打开对应相机的预编译好的程序：

         ```consle
         cd PrecompiledSamples
         ./XXXX_OpenCVSample
         ```

      ![设备连接](pic/ARMLinuxConnect.png)

      此时设备处于以太网广播连接建立的状态，侧面用于显示相机的状态的 LED 指示灯会呈**蓝色**并且常亮。

      ![BlueLed2](pic/BlueLed2.png)

      您可以参考[Scepter 软件开发包介绍](/zh-cn/ScepterSDK/Overview.md)了解相机的详细功能，开始探索相机。

    <!-- tabs:end -->

   <!-- tabs:end -->

<!-- tabs:start -->

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
