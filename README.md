# jetsonNsightProfiling
This repository contains a guide to do profiling on NVIDIA Jetson devices using the NVIDIA Nsight System.

## What do you need?
### Hardware Requirement
To profile workloads on a Jetson device, you need to have a Linux host running on x86 architecture hardware. 
### Software Requirement
On the host machine, you need to download the latest version of the [NVIDIA SDK Manager](https://developer.nvidia.com/nvidia-sdk-manager). 
Once the installation pack has been downloaded, go to the directory of the downloaded file, and run the following command to install the manager.
```sh
sudo apt install ./sdkmanager-[version].deb
```

And then use the following command to launch the SDK Manager.
```sh
sdkmanager
```

In the SDK Manager, you need to select the choose the platform that you are trying to profile and the Jetpack version that was installed on the Jetson device. It is very crucial to find the correct version of the Jetpack or L4T, otherwise you will not be able to launch your profiler due to incompatibility. For more information, there is a [discussion thread](https://forums.developer.nvidia.com/t/getting-target-is-not-supported-in-nvidia-nsight-systems-for-tx2/125704/7) about this requirement on the official NVIDIA Developer Forums. To find the correct Jetpack or L4T version, you will find this [tutorial](https://www.jetsonhacks.com/2017/08/28/quick-tip-which-version-of-l4t-is-running-nvidia-jetson-development-kit/) to be very helpful. 

Once you have selected the correct version and device, you could go through the steps to install all the required tools on your host machine. Once they are all installed, you should be ready to profile some workloads on your Jetson device. 

## How to do profiling?
### Use the NVIDIA Nsight Systems
We will use the NVIDIA Nsight Systems for profiling. It will be able to provide us with system wide hardware profiling. For Jetson devices, it is impossible to directly use this inside their own OS, so that is the reason why we need to use this additional host machine for profiling. For more information, there is also a [discussion thread](https://forums.developer.nvidia.com/t/tx2-nvidia-visual-profiler/64440/3) about this requirement on the official NVIDIA Developer Forums.

### Connect to the device
In the NVIDIA Nsight Systems, click on the tab of ```Select target for profiling...```, and choose ```Configure targets``` in the dorp-down menu. In the ```Manage targets``` window, click on ```Create a new connection``` to configure your connection to your Jetson device. If the host machine and the Jetson device are connected to the same network, you could just use the ```ifconfig``` command to find the IP address of your Jetson device. Once the configuration is done, click on ```Connect``` to connect to your Jetson device. The user that you use to connect to the device must have root access on the device, otherwise the profiling can not be proceeded. 

### Start profiling
Once you have connected to the device, you could start to configure your profiling setting. The most important settings are the ```Command line with argument```, which will be the command that you need to run your workloads, and the ```Working directory```, which will be the location will you wish to run your previous command to start your workload. Check all other options that you need such as the Collect CUDA trace. Once all the options are set, just click on the ```Start``` and profile your workloads.

### Viewing profiling results
To view the profiling results, you could just directly view it in the NVIDIA Nsight Systems on the host machine. Or you could transfer the profile results to other machines and view them with the latest [NVIDIA Nsight Systems](https://developer.nvidia.com/nsight-systems). 