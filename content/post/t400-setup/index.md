---
title: T400 mods
description: A collection of ways you can mod a Thinkpad T400
date: 2023-09-07 00:00:00+0000
image: thinkpad2.jpg
categories:
        - Thinkpad
        - Libreboot
tags:
        - thinkpad
        - libreboot
---
my daily driver is the Thinkpad T400, the most powerful laptop that you can libreboot to remove completely the proprietary Lenovo BIOS in favor of a fully open source BIOS. The distro on it its Parabola GNU/Linux-libre: a 100% free distribution.\
I have done a series of mods on this machine, and more are to come. What follows is a list of some useful resources on the T400 itself and the mods compatible with this device.

## Resources
- tons of info on the [Thinkpad T400](https://mcdojf.wixsite.com/t400)
- [Thinkpad T400 manual](https://thinkpads.com/support/hmm/hmm_pdf/43y6629_05.pdf)
- [Thinkpad T400 specs](https://www.thinkwiki.org/wiki/Category:T400)
- [Trustworthy site](https://minifree.org/) that sells Librebooted devices (including T400s)

## MODS
Here are the most common mods you can do on a Thinkpad T400
### Libreboot 
The Libreboot project provides free, open source (libre) boot firmware based on coreboot, replacing proprietary BIOS/UEFI firmware. I made a guide on how to do that. It's [here](https://bytemeifyoucan.lol/p/my-t400-libreboot-guide/).\
The Official Libreboot site is [this](https://libreboot.org/). The Thinkpad T400 official page is [this](https://libreboot.org/docs/hardware/t400.html).
#### Removal of proprietary hardware
After librebooting the T400 any hardware that requires proprietary blobs. In the case of this model you will most likely only need to replace the wifi card. One of the most suggested is the Atheros AR5BXB112 AR9380. It is a 3x3 450mbps WiFi card which works perfectly with free drivers and firmware, it should cost between 10 and 15 euros on Ebay or similar sites.\
[This](https://h-node.org/wifi/catalogue/en/1/1/undef/undef/yes?) is the complete list of cards approved by the Free Software Foundation.
### Quad-core mod
It is possible to install a series of quad-core processors on the T400, taking advantage of the fact that they have the same socket of the dual-core Core Duos that come with stock machine.\
You will need some soldering skills and decent amount of patience. A very well done guide can be found [here](https://thonkpeasant.xyz/guides/other/quad.html).\
The original post can be found [here](https://thinkpad-forum.de/threads/core2-quad-mit-coreboot-libreboot-auf-t500-wahrsch-auch-t400-benutzen-beta.199129/). (in german)
### Cooling mod 
Cooling mods really do exists out there, even tho I have never tried one on my T400s, considering i have heard mixed opinions about the actual improvements when it comes to the CPU degrees. Mileage may vary.\
All guides follow more or less the same principle: remove the metal sheeting from the plastic bottom casing and drill holes in the case. Examples of the procedures are [this](https://thonkpeasant.xyz/guides/other/cool.html) and [this](https://www.instructables.com/Fix-a-Thinkpad-T400s-Thermal-Issues-Once-and-For-/).
### bluetooth
The bluetooth of the T400 is 2.1, you can easily upgrade the bluetooth 4.0 by swapping the card located behind the LCD front bezel. Most recommended model is **Bluetooth 4.0 Genuine Lenovo FRU 60Y3305 60Y3303**.\
More info [here](https://www.thinkwiki.org/wiki/Bluetooth_Daughter_Card_slot).
### Ultra-bay mods
The most commond usage for the ultra bay, when a cd reader is not needed, is to use an Hard Drive caddy module to have a second 2.5 inch drive. Parts are easily available for about ten euros.
I am currently working on a variation of a mod I have seen floating around the world wide web. It's [this one](https://hackaday.com/tag/thinkpad-ultrabay/). In the article the laptop used is the T420 so I changing the 3D printed part to fit the T400 ultrabay.\
More info and **maybe** a guide will appear in the future, depending on how much time and effor i want to waste on this idea.
### Express Card slot
The T400 Express Card slot allows you to slot in any compatible Express Card 54 and by extension any Express Card 34. One common example is using a card with one or two (depending on the model) USB 3.0 plugs, with up to (i think) 5Gbps transfer speed.\
Other types of Express Cards can be found scattered around the web, from the classic card reader, to different post extensions to SD readers to even modules for eGPUs with awful performances.
### Screen replacement
The T400 has 14 inch TFT LCD display with resolutions of  either 1280x800 or 1440x900. The display backlight is eihter CCLF or LED. Detailed information about the diplays that can be found are [here](https://www.thinkwiki.org/wiki/TFT_display).
The LED model has a way better screen and is quite rare at this point, few are left on the marked. If you have the change, always go for the LED model.
### External WiFi antenna
Still have to do some research on this to understand if it makes sense or not.
### Opensource Battery
TODO
### USB C charging
TODO
### Thinklight mod
TODO
### Parabola GNU/Linux-libre
The distro i use on my librebooted T400 is Parabola GNU/Linux-libre, a community-driven, "labour-of-love" effort to maintain a 100% free (as in: freedom) operating system distribution that is lean, clean, and hackable.\
I made a guide on the manual installation of Parabola with an encrypted setup and Open-RC [here](https://bytemeifyoucan.lol/p/parabola-installation-guide/).

## The dock
TODO
