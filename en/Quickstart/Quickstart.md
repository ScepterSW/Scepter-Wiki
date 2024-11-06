## 1.Hardware Connection<!-- {docsify-ignore-all} -->

1. Mount the camera in a suitable fixture, such as a camera stand.

![DeviceConnection](../../zh-cn/Quickstart/Quickstart-asserts/01.png)

2. Provide 12~24V power to the camera through the multi-function cable (typical value: 12V 3A). Some models can use PoE+ power supply mode, please refer to the product specifications for details.

3. Connect the product to the host computer via an Ethernet cable. At this time, the device is in a state of Ethernet broadcast and no connection is established, and the LED indicator light on the side used to display the status of the camera will turn **blue** and flash repeatedly.

![BlueLed1](../../zh-cn/Quickstart/Quickstart-asserts/02.png)

4. Set the host IP address to be in the same network segment as the camera. The default IP of the device is **192.168.1.101**.

<!-- tabs:start -->

#### **Windows**

Set the local connection on Windows PC, set the subnet mask to 255.255.255.0, and set the IP address to the same network segment (such as 192.168.1.100).

<div class="center">

![WindowsStaticAddress](Quickstart-asserts/01.png)

</div>

<div class="center">

![WindowsStaticAddress](Quickstart-asserts/02.png)

</div>

<div class="center">

![WindowsStaticAddress](Quickstart-asserts/03.png)

</div>

#### **Ubuntu**

Set the local connection on Linux, set the subnet mask to 255.255.255.0, and set the IP address to the same network segment (such as 192.168.1.100).

<div class="center">

![LinuxEditConnections](Quickstart-asserts/04.png)

</div>

<div class="center">

![LinuxEdit](Quickstart-asserts/05.png)

</div>

<div class="center">

![LinuxStaticAddress](Quickstart-asserts/06.png)

</div>

#### **AArch64**

Set the local connection on ARM-Linux, set the subnet mask to 255.255.255.0, and set the IP address to the same network segment (such as 192.168.1.100). You can use nmtui to set it.

```consle
sudo nmtui
```

   <div class="center">

![ARMLinuxStaticAddress](../../zh-cn/Quickstart/Quickstart-asserts/09.png)

   </div>

<!-- tabs:end -->

> ① The network cards, routers, and switches used on the host side must meet the **Gigabit** requirements.
>
> ② When using multiple network cards, different IP network segments need to be set. This can cause network conflicts and connectivity issues when multiple network cards are configured for the same IP address range. In this case, if the connection between the host and the camera is interrupted, other devices may also be unable to establish or maintain a connection with the host due to IP address conflicts. To avoid this situation, each network card should be assigned a different IP network segment to ensure that every device on the network can communicate stably.

## 2.Device Open

Windows and Ubuntu18.04/20.04/22.04/24.04 users can download **ScepterGUITool** to explore the camera,

There is no graphical tool on the Ubuntu16.04 side, and the headless mode is commonly used on the AArch64 side. Users can download **ScepterSDK** to explore the camera:

 <!-- tabs:start -->

#### **ScepterGUITool**

ScepterGUITool download link:

<https://github.com/ScepterSW/ScepterGUITool>

or

<https://gitee.com/ScepterSW/ScepterGUITool>

You can download the Scepter development package through the following download methods:

Method 1: Downloads to local through git clone;

Method 2: Download the compressed package locally；

Method 3: Download the installer.

<!-- tabs:start -->

#### **Method 1**

① Open the download link, click Code, and copy the link;

```
git clone https://github.com/ScepterSW/ScepterGUITool
```

![git clone http](<../../zh-cn/Quickstart/Quickstart-asserts/10.png>)

② Open the terminal, enter the copied code and press Enter, and wait for the download to complete.

![get clone GUITool.png](<../../zh-cn/Quickstart/Quickstart-asserts/11.png>)

#### **Method 2**

open the **Releases** link, download the lastest version

Download link:

<https://github.com/ScepterSW/ScepterGUITool/releases>

or

<https://gitee.com/ScepterSW/ScepterGUITool/releases>

Taking v24.9.2 as an example, click Source code.

![GitHubGUITool](<../../zh-cn/Quickstart/Quickstart-asserts/12-1.png>)

![GitHubGUITool](<../../zh-cn/Quickstart/Quickstart-asserts/12-1-1.png>)

#### **Method 3**

Open the **Releases** link，download the lastest version.

Download link:

<https://github.com/ScepterSW/ScepterGUITool/releases>

or

<https://gitee.com/ScepterSW/ScepterGUITool/releases>

![GitHubGUITool](<../../zh-cn/Quickstart/Quickstart-asserts/12-1.png>)

<!-- tabs:start -->

#### **Windows**

**Download:** 

Taking v24.9.2 as an example, click ScepterGUITool_v24.9.2_windows_install.exe.

![GitHubGUITool](<../../zh-cn/Quickstart/Quickstart-asserts/12-2.png>)

**Install:** 

Double-click the xxx_install.exe locally，the default installed path is **C:\Users\user.name\AppData\Roaming\ScepterGUITool**.

![GitHubGUITool](<../../zh-cn/Quickstart/Quickstart-asserts/12-2-1.png>)

> Change the path with Browse.
>
> ![GitHubGUITool](<../../zh-cn/Quickstart/Quickstart-asserts/12-2-2.png>)
>
> Multi-install, choose overwrite or other path.
>
> ![GitHubGUITool](<../../zh-cn/Quickstart/Quickstart-asserts/12-2-8.png>)

Click Next.

![GitHubGUITool](<../../zh-cn/Quickstart/Quickstart-asserts/12-2-3.png>)

Click Next.

![GitHubGUITool](<../../zh-cn/Quickstart/Quickstart-asserts/12-2-4.png>)

Click Install.

![GitHubGUITool](<../../zh-cn/Quickstart/Quickstart-asserts/12-2-5.png>)

![GitHubGUITool](<../../zh-cn/Quickstart/Quickstart-asserts/12-2-6.png>)

Click Finish. Double-click the ScepterGUITool's icon in desktop，ro Double-click the ScepterGUITool in the installed path.

![GitHubGUITool](<../../zh-cn/Quickstart/Quickstart-asserts/12-2-7.png>)

#### **Ubuntu**

**Download:** 

Taking v24.9.2 as an example, click ScepterGUITool_v24.9.2_ubuntu_install.run.

![GitHubGUITool](<../../zh-cn/Quickstart/Quickstart-asserts/12-3.png>)

**Install:** 

Open the terminal and add the execution permission to xxx_install.run.

```
> sudo chmod +x ScepterGUITool_vXX.XX.XX_ubuntu_install.run
```

![GitHubGUITool](<../../zh-cn/Quickstart/Quickstart-asserts/12-3-1.png>)

```
> ./ScepterGUITool_vXX.XX.XX_ubuntu_install.run
```

![GitHubGUITool](<../../zh-cn/Quickstart/Quickstart-asserts/12-3-2.png>)

The installed path is **/home/username/ScepterGUITool/**

![GitHubGUITool](<../../zh-cn/Quickstart/Quickstart-asserts/12-3-3.png>)

Click the ScepterGUITool icon in left, or search the ScepterGUITool and click, or Double-click the ScepterGUITool in the installed path.

![GitHubGUITool](<../../zh-cn/Quickstart/Quickstart-asserts/12-3-4.png>)

<!-- tabs:end -->

<!-- tabs:end -->

ScepterGUITool includes the ScepterGUITool executable file and related dynamic link libraries.

<!-- tabs:start -->

#### **Windows**

![WindowsContents](../../zh-cn/Quickstart/Quickstart-asserts/13.png)

> When running ScepterGUITool for the first time, set permissions for the program to pass through the system firewall, as shown in the figure below.
>
>  <div class="center">
>
> ![WindowsFirewallSetting](Quickstart-asserts/07.png)
>
>  </div>

#### **Ubuntu**

![LinuxContents](../../zh-cn/Quickstart/Quickstart-asserts/15.png)

<!-- tabs:end -->

Double-click the ScepterGUITool executable file, run ScepterGUITool, and follow the steps below to connect the device:

① Search for devices.

![ScanDevice](../../zh-cn/Quickstart/Quickstart-asserts/16.png)

② Select the device you want to open.

![SelectDevice](../../zh-cn/Quickstart/Quickstart-asserts/17.png)

③ Click Connect to connect the device.

![ConnectDevice](../../zh-cn/Quickstart/Quickstart-asserts/18.png)

④ After the device is successfully connected, click the switch on the right side of Stream to start the camera's stream.

![DeviceStreamOn](../../zh-cn/Quickstart/Quickstart-asserts/19.png)

⑤ After successful startup, the image will appear on the right side.

![Image display](../../zh-cn/Quickstart/Quickstart-asserts/20.png)

⑥ At this time, the device is in the state where the Ethernet broadcast connection is established, and the LED indicator light on the side used to display the status of the camera will be **blue** and always on.

![BlueLed2](../../zh-cn/Quickstart/Quickstart-asserts/21.png)

You can refer to [ScepterGUITool introduction](/en/ScepterGUITool/Overview.md) to learn about the detailed functions of the camera and start exploring the camera.

#### **ScepterSDK**

ScepterSDK download link：

<https://github.com/ScepterSW/ScepterSDK>

or

<https://gitee.com/ScepterSW/ScepterSDK>

You can download the Scepter development package through the following download methods:

Method 1: Downloads to local through git clone;

Method 2: Download the compressed package locally.

<!-- tabs:start -->

#### **Method 1**

① Open the download link, click Code, and copy the link;

```
git clone https://github.com/ScepterSW/ScepterSDK
```

![git clone SDK http](<../../zh-cn/Quickstart/Quickstart-asserts/22.png>)

② Open the terminal, enter the copied code and press Enter, and wait for the download to complete.

![git clone ScepterSDK](<../../zh-cn/Quickstart/Quickstart-asserts/23.png>)

#### **Method 2**

Open the download link, click Code, and then click Download ZIP to download ScepterSDK locally.

If you want to use it under Ubuntu system, please make sure that the downloaded compressed package is decompressed under Ubuntu system. Do not copy and use it after decompression under Windows system.

![GitHub ScepterSDK](<../../zh-cn/Quickstart/Quickstart-asserts/24.png>)

<!-- tabs:end -->

ScepterSDK includes a series of friendly APIs, application sample programs and related dynamic link libraries.

![ARMLinuxContents](../../zh-cn/Quickstart/Quickstart-asserts/25.png)

Enter the AArch64/PrecompiledSamples folder and use the terminal to open the precompiled program for the corresponding camera:

```consle
cd PrecompiledSamples
./XXXX_OpenCVSample
```

![ARMLinuxConnect](../../zh-cn/Quickstart/Quickstart-asserts/26.png)

At this time, the device is in the state where the Ethernet broadcast connection is established, and the LED indicator light on the side used to display the status of the camera will be **blue** and always on.

![BlueLed2](../../zh-cn/Quickstart/Quickstart-asserts/21.png)

You can refer to [ScepterSDK introduction](/en/ScepterSDK/Overview.md) to learn about the detailed functions of the camera and start exploring the camera.

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
