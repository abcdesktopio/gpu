### Description
This method uses VirtualGL EGL backend to make Nvidia gpu acceleration possible for abcdesktop applications. Examples are based off https://github.com/selkies-project/docker-nvidia-egl-desktop

### Prerequisites

- Nvidia GPU driver 430.xx or later is properly installed on host.
- Fully functioning Kubernetes cluster with Nvidia Device Plugin installed 
https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/getting-started.html
- Nvidia Container Toolkit
https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html
- abcdesktop version 3.0

# Examples

- nvidia-smi app:
contains an fake X11 server(Xvfb) and all other neccessary dependencies. It can be used as a base for building other applications. This app starts an gnome-terminal where 'nvidia-smi', 'glxgears' and other testing programmes can be executed from

- chimerax is built on top of nvidia-smi app. It starts a konsole session, and executes 'vglrun' from the konsole. The args to the konsole needs to have '--hold' which keeps the application alive, and '-e' which starts the vglrun programme. 


### The VirtualGL EGL backend

VirtualGL faker supports EGL backend. (apps are tested with VGL v3.1) It eliminates the need for a 3D X server but still requires a 2D server.
Xvfb inside the application docker act as a headless 2D X server. Basically to start an application the following steps occur
- launch Xvfb
- export the X display of Xvfb instance
- export VGL_DISPLAY
- vglrun APPLICATION

VGL_DISPLAY in the Dockerfile needs to be set to 'egl'. This is the EGL device ID which identify a GPU. For multi-gpus, it can be spicified as egl0, egl1 etc..


### In the Dockerfile
- NVIDIA_VISIBLE_DEVICES all
- NVIDIA_DRIVER_CAPABILITIES all
 - VGL_DISPLAY egl
 
 


