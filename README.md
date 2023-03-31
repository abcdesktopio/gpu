## Description

This document is a craftpad to enable and share nvidia devices in kubernetes container 

## Goal

Run application like with nvidia support inside a container 
- glxgear
- chimestrax
- others 3D applications



## Issues

- Start more than one graphical container into the host 
https://forums.developer.nvidia.com/t/nvidia-gpu-0-failed-to-acquire-modesetting-permission/213267/4


## Design test-1

The host is a vm Ubuntu 20.04


##

enable nvidia gpu device to X.org 


### Run command `nvidia-container-cli`


```
nvidia-container-cli --load-kmods info
```

```
NVRM version:   525.105.17
CUDA version:   12.0

Device Index:   0
Device Minor:   0
Model:          NVIDIA GeForce GTX 1070
Brand:          GeForce
GPU UUID:       GPU-38ab400c-8953-69b1-5460-f70aefd40f8b
Bus Location:   00000000:0b:00.0
Architecture:   6.1
```

### Look for driver

#### what is headless ?

The term `headless` refers to a configuration in which the GPU does not send display information to a display monitor

```
apt-cache search nvidia-driver |grep server
```


### Run application in host 

### Run application in container
