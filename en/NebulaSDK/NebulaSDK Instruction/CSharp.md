# CSharp

## 概述

该 CSharp 软件包可用于 NebulaSDK 的深度、IR 和 RGB 数据的采集和处理。

## 环境要求

- .NET Framework : 4.6.x
- Visual Studio 2017

## 安装

- **安装 Vzense CSharp 软件包**

  - [安装 NebulaSDK](https://gitee.com/Vzense/NebulaSDK)

    ```console
    git clone https://gitee.com/Vzense/NebulaSDK.git
    ```

- **构建 CSharp 依赖的库环境**

  项目支持**x64**和**x86**，需要将相应的文件复制到'Bin/x64'或'Bin/x86'。 以**x64**为例：

- 方法一:

  手动将**NebulaSDK/Windows/Bin/x64**中的所有文件复制到**NebulaSDK/C#/Bin/x64**

- 方法二:

  运行**NebulaSDK/C#/install.py**

  ```console
  python install.py x64
  ```

## 说明

- NebulaSDK_CSharp.dll 是 NebulaSDK 的 CSharp 动态库
