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

Note: if run application as 'pod_application', environment var VGL_COMPRESS must be set to 'proxy' in Dockerfile. Alternatively, pass '-c proxy' to vglrun command. This is because when application run as pod, the DISPLAY variable in the pod will start with IP_ADDRESS_OR_USER_POD:0, on the other hand if application run as ephemeral container, the DISPLAY var is :0.0. 
If DISPLAY begins with a colon (“:”) or with “unix:”, then VirtualGL will assume that the X server connection is local and will enable the X11 Transport as the default. In some cases, however, the DISPLAY environment variable within the X proxy may not begin with a colon or “unix:”. In these cases, it is necessary to manually enable the X11 Transport by setting the VGL_COMPRESS environment variable to proxy or by passing an argument of -c proxy to vglrun
Ref: https://virtualgl.org/vgldoc/2_2_1/#hd008

### The VirtualGL EGL backend

VirtualGL faker supports EGL backend. (apps are tested with VGL v3.1) It eliminates the need for a 3D X server but still requires a 2D server.
Xvfb inside the application docker act as a headless 2D X server. Basically to start an application the following steps occur
- launch Xvfb
- export the X display of Xvfb instance
- export VGL_DISPLAY
- vglrun APPLICATION

VGL_DISPLAY in the Dockerfile needs to be set to 'egl'. This is the EGL device ID which identify a GPU. For multi-gpus, it can be specified as egl0, egl1 etc..


### In the Dockerfile
- NVIDIA_VISIBLE_DEVICES all
- NVIDIA_DRIVER_CAPABILITIES all
 - VGL_DISPLAY egl
 
 


