# Realtime-Hikvision-Preview-Python

preview **Hikvision** Ip Camera with python.

note: tested & verified on a docker container with ubuntu 20.04 as base 
image but should work on other platforms as well. you can use images 
from nvidia with cuda pre installed.

Getting started
===============

This module provides an interface to preview **Hikvision** Ip Camera with python, much faster than **opencv+RTSP**


Install
-------

- #### install pybind11
  - set pybind11 path in CMakeLists.txt if needed, you can use one of these commands to find its path 
  `locate pybind11 | grep Config.cmake` `locate pybind11 | grep config.cmake`

- ### download hikvision network sdk at(look sdk ready branch for pre downloaded sdk)
https://www.hikvision.com/en/support/download/sdk/device-network-sdk--for-linux-64-bit-/
  - extract and copy it to project dir
    - from sdk_folder(EN-HCNetSDKV6.1xxxx) copy lib to project dir
    - Modify the system preload and add a line of export: 

           vim ~/.bashrc
           export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:{absolute path in Linux corresponding to official dynamic library MakeAll}:{absolute path in Linux corresponding to official dynamic library MakeAll/HCNetSDKCom/}
           source ~/.bashrc
    - View configuration information

          cat /etc/ld.so.conf
    - If there is the following Include, it is recommended to create a new file setting under **ld.so.conf.d**, so that the isolation is relatively clean
include `ld.so.conf.d/*.conf`

          cd /etc/ld.so.conf.d
          vim hikvsdk.conf
          # Add the following 2 paths
          {The absolute path in Linux corresponding to the official dynamic library MakeAll}
          {absolute path of official dynamic library MakeAll/HCNetSDKCom/ in Linux}
    - After saving, execute the following command to reload the system.so configuration
`ldconfig`
    - example .bashrc and hikvsdk.conf are in the example folder take a look

  - #### install nvidia cuda
    - just google it you will find lots of information
    - in case of problems with cuda library path, set their directories for your system
    look at npp_cuda/CMakeLists.txt

  - #### config the CMakeLists.txt, set OpenCV_DIR, HIKVISION_INCLUDE, PYTHON_INCLUDE

  - copy all necessary librarys to ./lib or add the pathes to link_directories

  - make the project
    
    - in the project dir `mkdir build && cd build`
    - `cmake ..`
    - `make`
    - your files should be in `build/lib`

Usage
=====

```python
import HKIPcamera
import numpy as np

hkipc = HKIPcamera.HKIPCamera()

# login
login_success = hkipc.login(ip, name, password, port, channel, streamtype, linkmode=link_mode, device_id = device_id, bufferize=5)

# read frame and cast to ndarray
frame = hkipc.getframe()
frame = np.array(frame)

hkipc.release()
```