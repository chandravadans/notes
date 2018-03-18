# Notes of a distrohopper

## Ubuntu

### Pros 
* Everything works fine, works well(ish) with Nvidia Optimus setups.

### Cons
* Can't switch from Nvidia to intel on the fly. Need to logout/login.
* Horrible screen tearing while using Nvidia.
* Not a fan of adding endless PPAs.

### Misc
* 18.x is doing away with Unity, gnome's coming. Need to see how that works out.

## Fedora

### Pros
* Bleeding edge software, kernels.
* Easy to get Nvidia up and running.

### Cons
* No easy way of getting Optimus to work, using negativeio's repo results in an always on Nvidia card.
* Wayland is a pain!

## Misc
* Don't attempt to use bumblebee. Tons of issues.

## Manjaro

## Pros
* Nvidia optimus is perfect! bumblebee works like a charm!
* Rolling release, so no 'os updates'
* More stable than Arch (Or so they say)

## Cons
* Some manjaro community distro isos are not hybrid, fail to boot from usb when secureboot/uefi is enabled. 
Tried both, dd and rufus.
