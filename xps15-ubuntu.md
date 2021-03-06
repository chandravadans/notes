# Ubuntu 16.04.3

Installing ubuntu 16.04.3 on Dell XPS 15-9560

* 16GB RAM
* 512GB SSD
* Core i7-7700HQ
* Nvidia 1050, 4GB

## 1. Running the live usb

* Burn iso image to pendrive (Rufus on Win, dd on another linux)
* Boot, and if you get a problem about cpu#x being softblocked then at the grub command line (Try Ubuntu without installing -> 'o')
append this to the line that starts with 'linux':

```
nouveau.modeset=0
```

## 2. Nvidia + Intel graphics

* Get all availabe updates
* Add the graphics drivers ppa
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

### 1.1 Advantages of intel
* Super long battery life (8h)
* No video tearing
* Runs cool.

### 1.2 Advantages of nvidia
* Cuda!

### 1.3 Cuda
* Download the cuda 9.0 repository from Nvidia's developer [site](https://developer.nvidia.com/cuda-90-download-archive). Cuda 9.0 is the latest that can run on 16.04 as of Feb '18, because 384.11 is the latest proprietary driver in the repositories.

* After installing, do an update and install `cuda-toolkit-9.0`
 * Do *not* install plain `cuda` or `cuda-9_0`, both of them uninstall the installed proprietary driver and install the latest available version.
 
 * The files are installed at `/usr/local/cuda`, so try compiling the samples provided after copying them to somewhere writable, `/home/user` for example.
 
 * Check cuda installation by running one of the simple examples, `deviceQuery`
 
 Successful run:
 ```
 ./bin/x86_64/linux/release/deviceQuery Starting...

 CUDA Device Query (Runtime API) version (CUDART static linking)

Detected 1 CUDA Capable device(s)

Device 0: 
...
...
...
  Compute Mode:
     < Default (multiple host threads can use ::cudaSetDevice() with device simultaneously) >

deviceQuery, CUDA Driver = CUDART, CUDA Driver Version = 9.0, CUDA Runtime Version = 9.0, NumDevs = 1
Result = PASS
```

* If you get an error saying the cuda driver version isn't sufficient for the cuda runtime, you most likely installed `cuda` or `cuda-9_0` and it overwrote `nvidia-384` with something else.

### 1.4 Unsolved issues
* Horrible screen tearing when nvidia enabled. Most of the solutions ask you to add `TearFree=True` to xorg.conf, but that doesn't seem to help a lot.
 * This doesn't seem to be present in the latest driver `nvidia-390` but too bad the proprietary version isn't in the repos yet :(. You can, of course go the route of downloading the runfile from nvidia's site but I'd much rather wait for it to pop up in the repositories.

## 2. Power management

Battery is massive (97Wh) so that's awesome. Additional things possible include installing tlp.

## 3. Multi touch and gestures

Check the excellent guide on [reddit](https://www.reddit.com/r/Dell/comments/646y0t/xps_9560_setting_up_multitouch_gestures_with/)
