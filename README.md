## Description

This document is a craftwork to enable and share nvidia devices in kubernetes container 

## Goal

Run application like with nvidia support inside a container 
- glxgear
- chimestrax
- others 3D applications

Start more than one graphical container into the host 
It seems to works

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

## Description
2
​
3
This document is a craftwork to enable and share nvidia devices in kubernetes container 
4
​
5
## Goal
6
​
7
Run application like with nvidia support inside a container 
8
- glxgear
9
- chimestrax
10
- others 3D applications
11
​
12
Start more than one graphical container into the host 
13
It seems to works
15
https://forums.developer.nvidia.com/t/nvidia-gpu-0-failed-to-acquire-modesetting-permission/213267/4
16
​
17
​
18
## Design test-1
19
​
20
​
21
​
22
The host is a vm Ubuntu 20.04
23
​
24
​
25
### Run command `lspci | grep VGA`
26
​
27
enable nvidia gpu device to X.org 
28
​
29
```
30
lspci | grep VGA
31
```
32
​
33
```
34
00:0f.0 VGA compatible controller: VMware SVGA II Adapter
35
0b:00.0 VGA compatible controller: NVIDIA Corporation GP104 [GeForce GTX 1070] (rev a1)
36
```
37
​
38
​
39
​
40
​
41
### Look for driver
42
​
43
​
44
the term "headless" refers to a configuration in which the GPU does not send display information to a display monitor
45
​

46
```
47
apt-cache search nvidia-driver |grep server
48
```
49
​
50
```
51
xserver-xorg-video-nvidia-390 - NVIDIA binary Xorg driver
52
nvidia-driver-450-server - NVIDIA Server Driver metapackage
53
nvidia-driver-470-server - NVIDIA Server Driver metapackage
54
nvidia-driver-510-server - Transitional package for nvidia-driver-515-server
55
nvidia-driver-515-server - NVIDIA Server Driver metapackage
56
nvidia-driver-525-server - NVIDIA Server Driver metapackage
57
nvidia-headless-450-server - NVIDIA headless metapackage
58
nvidia-headless-470-server - NVIDIA headless metapackage
59
nvidia-headless-515-server - NVIDIA headless metapackage
60
nvidia-headless-525-server - NVIDIA headless metapackage
61
nvidia-headless-no-dkms-450-server - NVIDIA headless metapackage - no DKMS
62
nvidia-headless-no-dkms-470-server - NVIDIA headless metapackage - no DKMS
63
nvidia-headless-no-dkms-515-server - NVIDIA headless metapackage - no DKMS
64
nvidia-headless-no-dkms-525-server - NVIDIA headless metapackage - no DKMS
65
xserver-xorg-video-nvidia-435 - Transitional package for xserver-xorg-video-nvidia-455
66
xserver-xorg-video-nvidia-440 - Transitional package for xserver-xorg-video-nvidia-450
67
xserver-xorg-video-nvidia-450-server - NVIDIA binary Xorg driver
68
xserver-xorg-video-nvidia-470 - NVIDIA binary Xorg driver
69
xserver-xorg-video-nvidia-470-server - NVIDIA binary Xorg driver
70
xserver-xorg-video-nvidia-510 - NVIDIA binary Xorg driver
71
xserver-xorg-video-nvidia-515 - NVIDIA binary Xorg driver
72
xserver-xorg-video-nvidia-515-server - NVIDIA binary Xorg driver
73
xserver-xorg-video-nvidia-525 - NVIDIA binary Xorg driver
74
xserver-xorg-video-nvidia-525-server - NVIDIA binary Xorg driver
75
nvidia-driver-418-server - NVIDIA Server Driver metapackage
76
nvidia-driver-440-server - Transitional package for nvidia-driver-450-server
```


### Run application in host 

### Run application in container
