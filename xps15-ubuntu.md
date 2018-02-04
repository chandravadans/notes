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

```

