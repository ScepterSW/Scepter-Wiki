# 3.1 Python

Python 软件包是 Vzense Nebula API 的开源项目。

该 Python 软件包可帮助开发者通过 python 方法轻松使用 Vzense ToF 相机。

## 3.1.1 环境要求

- python 版本 : 3.7.x
- python 模块 : ctypes, numpy, opencv-python(仅用于显示)

## 3.1.2 目录

- **DS77**: DS77Lite/DS77Pro 的 API 和示例代码
- **DS77C**: DS77CLite/DS77CPro 的 API 和示例代码
- **DS86**: DS86 & DS87 的 API 和示例代码

## 3.1.3 快速开始

1. 安装模块:

```console
   pip install numpy
   pip install opencv-python
```

2. 切换到产品目录下的 Samples 目录，运行您需要的示例。
   例如，转到 DS77/Samples/FrameViewer，然后运行“python FrameViewer_DS77.py”

3. 当使用多个网卡时，需要设置不同的 IP 网段。
