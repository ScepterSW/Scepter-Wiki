# 3.1.2. 项目配置

在运行 ScepterSDK 之前，请确保您的 Python 版本为 3.7.x 或更高版本，并已安装 ctypes、numpy 模块。

```console
pip install numpy
```

使用 Scepter SDK 开发新的项目，需要使用英文路径。针对不同的操作系统，需要同时复制 SDK 中的 Python 文件夹和对应系统的文件夹。API 文件夹中的 Scepter_api.py 会自动读取相机的 libScepter_api.so 或 Scepter_api.dll 库文件。

```python
if system_ == 'linux':
   if machine_ == 'x86_64':
      os_info = os.uname()
      print('os_info:',type(os_info))
      system_info = os_info.version
      print('version:',system_info)
      if system_info.find('18.04') != -1 or system_info.find('20.04') != -1:
         libpath = (os.path.abspath(os.path.dirname(os.getcwd()) + os.path.sep + "../../../"))+"/Ubuntu18.04/Lib/libScepter_api.so"
         print(libpath)
         self.vz_cam_lib = cdll.LoadLibrary(libpath)
      else:
         libpath = (os.path.abspath(os.path.dirname(os.getcwd()) + os.path.sep + "../../../"))+"/Ubuntu16.04/Lib/libScepter_api.so"
         print(libpath)
         self.vz_cam_lib = cdll.LoadLibrary(libpath)
      elif machine_ == 'aarch64':
         libpath = (os.path.abspath(os.path.dirname(os.getcwd()) + os.path.sep + "../../../"))+"/AArch64/Lib/libScepter_api.so"
         print(libpath)
         self.vz_cam_lib = cdll.LoadLibrary(libpath)
   else:
      print('do not supported OS', system_, machine_)
      exit()
elif platform.system() == 'Windows':
   if machine_ == 'amd64':
      if architecture_ == '64bit':
         libpath = (os.path.abspath(os.path.dirname(os.getcwd()) + os.path.sep + "../../../"))+"/Windows/Bin/x64/Scepter_api.dll"
         print(libpath)
         elf.vz_cam_lib = cdll.LoadLibrary(libpath)
   else:
      libpath = (os.path.abspath(os.path.dirname(os.getcwd()) + os.path.sep + "../../../"))+"/Windows/Bin/x86/Scepter_api.dll"
      print(libpath)
      self.vz_cam_lib = cdll.LoadLibrary(libpath)
   else:
      print('do not supported OS', system_, machine_)
      exit()
else:
   print('do not supported OS', system_, machine_)
   exit()

```
