---
title: "GoPro-Eye, vision analysis of coffee bean roasts"
date: 2026-03-14
draft: false
tags: ["coffee-roasting", "computer-vision", "gopro", "ai-vision", "usb"]
---

In my [previous post about r1-eye](https://briancarroll.cool/projects/r1-eye/), I described using a jailbroken Rabbit R1 to watch my coffee roasts and send images to Claude Vision for analysis. It worked but there are 2 issues I found when trying to place the camera for the best shot. The first is that there is nothing you can use to mount the r1. I used stacked cardboard boxes which I constantly bumped. The second is the bright orange frame of the r1. The reflection skewed the color of all the images and we had to resort to a cropping mechanism to remove it.

I had a GoPro Hero 13 laying around, which I can mount on a tripod, and decided to see if that would work.

It took an hour or so to get it running. The sentinel architecture is the same. Artisan sends roast events over WebSocket, the sentinel orchestrates captures based on phase and timing, and Claude Vision scores each image. 

What changed is the device layer underneath. Instead of ADB, I'm using the USB NCM to:

1. Send an HTTP shutter command to the GoPro over USB NCM.
2. Download the photo directly from the camera’s SD card over the same USB connection, then delete it to free space.

A few things I found interesting were:

**The Hero 13 has an mDNS bug.** The camera doesn’t advertise its `_gopro-web` service like it’s supposed to, so the SDK can’t auto-discover it. You have to pass the camera’s serial number manually. 

**USB-C as a network adapter is neat.** The GoPro uses USB NCM (Network Control Model) to present itself as an ethernet device. Your computer gets assigned an IP on a subnet, and the camera listens on port 8080. It’s HTTP over USB.

**The image quality jump.** Going from the R1’s 8MP with a quadrant crop to remove the orange frame to 27MP gives Claude Vision much better input. Development scores are noticeably more consistent now.

Anyway I am playing around with the GoPro version and have yet to analyze the 2 roasts I just completed with it.

GitHub: [github.com/frogmoses/gopro](https://github.com/frogmoses/gopro)
