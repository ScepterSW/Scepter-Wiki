## 1.Hardware Connection<!-- {docsify-ignore-all} -->

1. Mount the camera in a suitable fixture, such as a camera stand.

![DeviceConnection](../../zh-cn/Quickstart/pic/DeviceConnection.png)

2. Provide 12~24V power to the camera through the multi-function cable (typical value: 12V 3A). Some models can use PoE+ power supply mode, please refer to the product specifications for details.

3. Connect the product to the host computer via an Ethernet cable. At this time, the device is in a state of Ethernet broadcast and no connection is established, and the LED indicator light on the side used to display the status of the camera will turn **blue** and flash repeatedly.

![BlueLed1](../../zh-cn/Quickstart/pic/BlueLed1.png)

4. Set the host IP address to be in the same network segment as the camera. The default IP of the device is **192.168.1.101**.

<!-- tabs:start -->

#### **Windows**

Set the local connection on Windows PC, set the subnet mask to 255.255.255.0, and set the IP address to the same network segment (such as 192.168.1.100).

<div class="center">

![WindowsStaticAddress](pic/WindowsStaticAddress1.png)

</div>

<div class="center">

![WindowsStaticAddress](pic/WindowsStaticAddress2.png)

</div>

<div class="center">

![WindowsStaticAddress](pic/WindowsStaticAddress3.png)

</div>

#### **Ubuntu**

Set the local connection on Linux, set the subnet mask to 255.255.255.0, and set the IP address to the same network segment (such as 192.168.1.100).

<div class="center">

![LinuxEditConnections](pic/LinuxEditConnections1.png)

</div>

<div class="center">

![LinuxEdit](pic/LinuxEdit2.png)

</div>

<div class="center">

![LinuxStaticAddress](pic/LinuxStaticAddress3.png)

</div>

#### **AArch64**

Set the local connection on ARM-Linux, set the subnet mask to 255.255.255.0, and set the IP address to the same network segment (such as 192.168.1.100). You can use nmtui to set it.

```consle
sudo nmtui
```

   <div class="center">

![ARMLinuxStaticAddress](../../zh-cn/Quickstart/pic/ARMLinuxStaticAddress.png)

   </div>

<!-- tabs:end -->

> ① The network cards, routers, and switches used on the host side must meet the **Gigabit** requirements.
>
> ② When using multiple network cards, different IP network segments need to be set. This can cause network conflicts and connectivity issues when multiple network cards are configured for the same IP address range. In this case, if the connection between the host and the camera is interrupted, other devices may also be unable to establish or maintain a connection with the host due to IP address conflicts. To avoid this situation, each network card should be assigned a different IP network segment to ensure that every device on the network can communicate stably.

## 2.Device Open

Windows and Ubuntu18.04/20.04/22/04 users can download **ScepterGUITool** to explore the camera,

There is no graphical tool on the Ubuntu16.04 side, and the headless mode is commonly used on the AArch64 side. Users can download **ScepterSDK** to explore the camera:

 <!-- tabs:start -->

#### **ScepterGUITool**

ScepterGUITool download link:

<https://github.com/ScepterSW/ScepterGUITool>

or

<https://gitee.com/ScepterSW/ScepterGUITool>

You can download the Scepter development package through the following download methods:

Method 1: Downloads to local through git clone;

Method 2: Download the compressed package locally.

<!-- tabs:start -->

#### **Method 1**

① Open the download link, click Code, and copy the link;

```
git clone https://github.com/ScepterSW/ScepterGUITool
```

![git clone http](<../../zh-cn/Quickstart/pic/git clone http.png>)

② Open the terminal, enter the copied code and press Enter, and wait for the download to complete.

![get clone GUITool.png](<../../zh-cn/Quickstart/pic/git clone GUITool.png>)

#### **Method 2**

Open the download link, click Code, and then click Download ZIP to download the ScepterGUITool compressed package locally.

![GitHubGUITool](<../../zh-cn/Quickstart/pic/GitHub GUITool.png>)

<!-- tabs:end -->

ScepterGUITool includes the ScepterGUITool executable file and related dynamic link libraries.

<!-- tabs:start -->

#### **Windows**

![WindowsContents](../../zh-cn/Quickstart/pic/WindowsContents.png)

> When running ScepterGUITool for the first time, set permissions for the program to pass through the system firewall, as shown in the figure below.
>
>  <div class="center">
>
> ![WindowsFirewallSetting](pic/WindowsFirewallSetting.png)
>
>  </div>

#### **Ubuntu**

![LinuxContents](../../zh-cn/Quickstart/pic/LinuxContents.png)

<!-- tabs:end -->

Double-click the ScepterGUITool executable file, run ScepterGUITool, and follow the steps below to connect the device:

① Search for devices.

![ScanDevice](../../zh-cn/Quickstart/pic/ScanDevice.png)

② Select the device you want to open.

![SelectDevice](../../zh-cn/Quickstart/pic/SelectDevice.png)

③ Click Connect to connect the device.

![ConnectDevice](../../zh-cn/Quickstart/pic/ConnectDevice.png)

④ After the device is successfully connected, click the switch on the right side of Stream to start the camera's stream.

![DeviceStreamOn](../../zh-cn/Quickstart/pic/DeviceStreamOn.png)

⑤ After successful startup, the image will appear on the right side.

![Image display](../../zh-cn/Quickstart/pic/DisplayArea.png)

⑥ At this time, the device is in the state where the Ethernet broadcast connection is established, and the LED indicator light on the side used to display the status of the camera will be **blue** and always on.

![BlueLed2](../../zh-cn/Quickstart/pic/BlueLed2.png)

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

![git clone SDK http](<../../zh-cn/Quickstart/pic/git clone SDK http.png>)

② Open the terminal, enter the copied code and press Enter, and wait for the download to complete.

![git clone ScepterSDK](<../../zh-cn/Quickstart/pic/git clone ScepterSDK.png>)

#### **Method 2**

Open the download link, click Code, and then click Download ZIP to download ScepterSDK locally.

If you want to use it under Ubuntu system, please make sure that the downloaded compressed package is decompressed under Ubuntu system. Do not copy and use it after decompression under Windows system.

![GitHub ScepterSDK](<../../zh-cn/Quickstart/pic/GitHub ScepterSDK.png>)

<!-- tabs:end -->

ScepterSDK includes a series of friendly APIs, application sample programs and related dynamic link libraries.

![ARMLinuxContents](../../zh-cn/Quickstart/pic/ARMLinuxContents.png)

Enter the AArch64/PrecompiledSamples folder and use the terminal to open the precompiled program for the corresponding camera:

```consle
cd PrecompiledSamples
./XXXX_OpenCVSample
```

![ARMLinuxConnect](../../zh-cn/Quickstart/pic/ARMLinuxConnect.png)

At this time, the device is in the state where the Ethernet broadcast connection is established, and the LED indicator light on the side used to display the status of the camera will be **blue** and always on.

![BlueLed2](../../zh-cn/Quickstart/pic/BlueLed2.png)

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
