## Description

This document is a craftpad to enable and share nvidia devices in kubernetes container 

## Goal

Run application like with nvidia support inside a container 
- glxgear
- chimestrax
- others 3D applications


## Issues

- Start more than one graphical container into the host 
- Read 
https://forums.developer.nvidia.com/t/nvidia-gpu-0-failed-to-acquire-modesetting-permission/213267/4

## Install 

### Def

#### what is `headless` ?

The term `headless` refers to a configuration in which the GPU does not send display information to a display monitor

#### what is `dkms` 
Dynamic Kernel Module Support (DKMS) is a program/framework that enables generating Linux kernel modules whose sources generally reside outside the kernel source tree. The concept is to have DKMS modules automatically rebuilt when a new kernel is installed.


## Design test-1

The host is a vm Ubuntu 20.04

![gpu-abcdesktop-desing-test-1](gpu-abcdesktop-infra.svg)


## Install

### TEST: Start more than on Xorg server and use nvidia-smi 

Start Xorg server on DISPLAY from 0 to 4

```
Xorg :0 &
Xorg :1 &
Xorg :2 &
Xorg :3 &
Xorg :4 &
```

We should have five Xorg processes

```
nvidia-smi
```

Command result

```
Sat Apr  1 07:37:02 2023      
+---------------------------------------------------------------------------------------+
| NVIDIA-SMI 530.30.02              Driver Version: 530.30.02    CUDA Version: 12.1     |
|-----------------------------------------+----------------------+----------------------+
| GPU  Name                  Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf            Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                                         |                      |               MIG M. |
|=========================================+======================+======================|
|   0  NVIDIA GeForce GTX 1070         On | 00000000:0B:00.0 Off |                  N/A |
|  0%   31C    P8                8W / 180W|     39MiB /  8192MiB |      0%      Default |
|                                         |                      |                  N/A |
+-----------------------------------------+----------------------+----------------------+
                                                                                         
+---------------------------------------------------------------------------------------+
| Processes:                                                                            |
|  GPU   GI   CI        PID   Type   Process name                            GPU Memory |
|        ID   ID                                                             Usage      |
|=======================================================================================|
|    0   N/A  N/A   1137144      G   /usr/lib/xorg/Xorg                            5MiB |
|    0   N/A  N/A   1138330      G   /usr/lib/xorg/Xorg                            5MiB |
|    0   N/A  N/A   1138664      G   /usr/lib/xorg/Xorg                            5MiB |
|    0   N/A  N/A   1138670      G   /usr/lib/xorg/Xorg                            5MiB |
|    0   N/A  N/A   1138676      G   /usr/lib/xorg/Xorg                            5MiB |
+---------------------------------------------------------------------------------------+
```

> All XOrg process are shring the SAME PID namespace and nvidia-smi has capability to list process.


### Install kubernetes 

https://docs.nvidia.com/datacenter/cloud-native/kubernetes/install-k8s.html

- Option 2: Installing Kubernetes Using Kubeadm
- Choose containerd

### Install NVIDIA Device Plugin

https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/getting-started.html


## NVIDIA package description

| Package name               | Description | 
|----------------------------|-------------|
| nvidia-driver-xxx          | The full driver package, kernel driver, 2D/3D xorg driver, cuda driver, utilities|
| nvidia-headless-xxx        | only kernel driver, cuda driver, utilities for compute servers without desktop|
| nvidia-headless-no-dkms-xxx| same as -headless but without dkms dependency so the kernel modules won’t be compiled automatically|




## Check the result of command `nvidia-container-cli`


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


### Run application in host 

### Run application in container
