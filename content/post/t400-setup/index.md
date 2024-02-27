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

# thinkpad t400 setup

my daily driver is the Thinkpad T400, the most powerful laptop that you can libreboot to remove completely the propietary Lenovo BIOS in favor of a fully open source BIOS.

some info on the [Thinkpad T400](https://mcdojf.wixsite.com/t400)

# MODS
Here are the most common mods you can do on a Thinkpad T400
## Libreboot 
The Libreboot project provides free, open source (libre) boot firmware based on coreboot, replacing proprietary BIOS/UEFI firmware. I made a guide on how to do that.
## Quad-core mod
It is possible to install a series of quad-core processors on the T400, taking advantage of the fact that they have the same socket of the dual-core Core Duos that come with stock machine.\
You will need some soldering skills and decent amount of patience. A very well done guide can be found [here](https://thonkpeasant.xyz/guides/other/quad.html).\
The original post can be found [here](https://thinkpad-forum.de/threads/core2-quad-mit-coreboot-libreboot-auf-t500-wahrsch-auch-t400-benutzen-beta.199129/). (in german)
## Cooling mod 
TODO
## bluetooth
the bluetooth of the T400 is 2.1, you can easily upgrade the bluetooth 4.0 easily by swapping the card located behind the LCD front bezel
## Ultra-bay mod
TODO: who the fuck knows if i will ever do this
## Express Card slot
The T400 Express Card slot allows you to slot in any compatibile Express Card 54, i think the most used card is the one that gives you one or two (depending on the model) USB 3.0 plugs, with up to (i think) 5Gbps transfert speed. Cool shit.
## Parabola GNU/Linux-libre
The distro i use on my librebooted T400 is Parabola GNU/Linux-libre, a community-driven, "labour-of-love" effort to maintain a 100% free (as in: freedom) operating system distribution that is lean, clean, and hackable.
A guide on installing parabola with a encrypted root partition using luks and open-rc could be created in the future.

