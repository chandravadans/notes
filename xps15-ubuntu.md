# Ubuntu 16.04.3

* 16GB RAM
* 512GB SSD
* Core i7-7700HQ
* Nvidia 1050, 4GB

## Nvidia + Intel graphics

* Get all availabe updates
* Add graphics drivers ppa
```
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt-get update
```
* Open additional drivers, install the latest proprietary driver (nvidia-384 as of Feb 18)
* Change `GRUB_CMDLINE_LINUX_DEFAULT` in `/etc/default/grub` to the following:
```
GRUB_CMDLINE_LINUX_DEFAULT="quiet acpi_rev_override=5"

```
* Run `sudo update-grub`.
* Reboot, enjoy. Whenever you want to switch to nvidia, change the PRIME profile in the nvidia-settings app to nvidia.
Log back in, and there it is!

* Two ways to check what card is getting used:

Install `mesa-utils` first. Then,

1. `glxinfo|grep string`
 
If using intel,
```
server glx vendor string: SGI
server glx version string: 1.4
client glx vendor string: Mesa Project and SGI
client glx version string: 1.4
OpenGL vendor string: Intel Open Source Technology Center
OpenGL renderer string: Mesa DRI Intel(R) HD Graphics 630 (Kaby Lake GT2) 
OpenGL core profile version string: 4.5 (Core Profile) Mesa 17.2.4
OpenGL core profile shading language version string: 4.50
OpenGL version string: 3.0 Mesa 17.2.4
OpenGL shading language version string: 1.30
OpenGL ES profile version string: OpenGL ES 3.2 Mesa 17.2.4
OpenGL ES profile shading language version string: OpenGL ES GLSL ES 3.20
```

And if using Nvidia,
```
server glx vendor string: NVIDIA Corporation
server glx version string: 1.4
client glx vendor string: NVIDIA Corporation
client glx version string: 1.4
OpenGL vendor string: NVIDIA Corporation
OpenGL renderer string: GeForce GTX 1050/PCIe/SSE2
OpenGL core profile version string: 4.5.0 NVIDIA 384.111
OpenGL core profile shading language version string: 4.50 NVIDIA
OpenGL version string: 4.5.0 NVIDIA 384.111
OpenGL shading language version string: 4.50 NVIDIA
OpenGL ES profile version string: OpenGL ES 3.2 NVIDIA 384.111
OpenGL ES profile shading language version string: OpenGL ES GLSL ES 3.20
```

2. `glxgears`

If using intel,
```
Running synchronized to the vertical refresh.  The framerate should be
approximately the same as the monitor refresh rate.
304 frames in 5.0 seconds = 60.717 FPS
300 frames in 5.0 seconds = 59.936 FPS
300 frames in 5.0 seconds = 59.935 FPS
300 frames in 5.0 seconds = 59.932 FPS
300 frames in 5.0 seconds = 59.936 FPS
```

And if using nvidia,
```
Running synchronized to the vertical refresh.  The framerate should be
approximately the same as the monitor refresh rate.
106046 frames in 5.0 seconds = 21208.211 FPS
109502 frames in 5.0 seconds = 21898.959 FPS
102100 frames in 5.0 seconds = 20419.551 FPS
106430 frames in 5.0 seconds = 21285.924 FPS
108434 frames in 5.0 seconds = 21686.387 FPS
```

### Advantages of intel
* Super long battery life (8h)
* No video tearing
* Runs cool.

### Advantages of nvidia
* Cuda!
