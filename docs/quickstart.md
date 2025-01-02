# Quick Start Guide

The goal of this quick start guide is to connect the EchoTherm module to a host desktop Linux system and demonstrate a video feed.

!!! info
    
    These instructions were developed and tested on an Ubuntu 22.04 LTS physical machine with a monitor. This guide is not meant for headless embedded systems, it is intended to provide a real-time display.

## Prerequisites

You system must have git and build-essential packages (most likely already installed)
```
sudo apt update
sudo apt install git-all
sudo apt install build-essential
```

## Quick Start Steps

1. Clone the repo and run the install script

```
git clone https://github.com/EchoMAV/EchoTherm-Daemon.git
cd EchoTherm-Daemon
sudo ./install.sh
```
2. Reboot the machine  
3. Run the echotherm damon
```
echothermd --daemon
```
3. Plug in the EchoTherm Module via the provided USB cable and USB backplate.
4. List your VideoForLinux devices to identify the camera endpoint:
```
v4l2-ctl --list-devices  
```
!!! note 
    Take note of the device endpoint (e.g. `/dev/video0`) and use it in the next step as {Device id}. Depending on your machine setup, the device may be called >`Dummy video device` or `EchoTherm Loopback device`  

5. View the video on your desktop:
```
gst-launch-1.0 v4l2src device={Device id} ! videoconvert ! autovideosink
```
6. In another terminal window, use the `echotherm` app to change camera settings, e.g. to change the color palette:
```
echotherm --colorPalette 4
```

Congrats! You now have a functional camera. For more software details, visit the [EchoTherm-Daemon Repo](https://github.com/EchoMAV/EchoTherm-Daemon) and/or continue reading these docs.

