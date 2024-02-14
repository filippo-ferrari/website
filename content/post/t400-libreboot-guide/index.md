---
title: My T400 Libreboot Guide
description: Simplest Libreboot guide I can write
date: 2024-01-22 00:00:00+0000
image: libreboot.png
categories:
    - Libreboot
    - Thinkpad
tags:
    - libreboot
    - thinkpad
    - bios
---

[DRAFT] // It's a fucking DRAFT, WAIT

# The bestest most amazing T400 setup possible

**T400? Why? TODO**

The first step is to flash libreboot on your T400, the libreboot docs have a ton of information about installing libreboot on any compatible device, but I found it confusing to read given the huge amount of information on the site and the way they are structured. If you're not yet knowledgeable on the matter and you "just" want to libreboot your T400 (or X200), you might want to follow a simpler guide with just the must-know information and not much else.

## What hardware is needed:

1. Some type of programmer: The two most common programmers that I would suggest are either a Raspberry Pi or the CH341A programmer. The case for the Pi is that if you just plan to flash your device, you will afterward still have a usable Pi with a lot of potential for homemade projects. The case of the CH341A is that it is inexpensive (I paid around 5 bucks for it). Still, when you're done, you won't have any use for the CH341A unless you want to flash other devices with an SPI interface.

   Given my personal experience, I would suggest the CH341A simply because I tried and tried to flash my T400 with Pi 4 B without any luck. I was not able to read from the chip at any time, though after more research, I think these issues might be due to my clip.

   It's important to be aware that there are multiple versions of the CH341A programmer, the most common one being a version that delivers 3.3 volts to the motherboard chip, a voltage that is too big and could potentially fry the chip (even though multiple people have used it with no issue). If you opt for the CH341A and want to be as safe as possible, you must consider either finding the model that delivers 1.8V or modding the standard 3.3v version for 1.8v delivery. How: [LINK]

2. SOIC clip: You will need a SOIC clip to connect to the flash chip and the programmer. I cannot stress enough how important the quality of the clip is. I have struggled for weeks to make awful Chinese clips work due to me being a cheap fuck, but I assure that a good clip is gonna make the process simpler and less frustrating. The best and most quoted clip is the POMONA clip, which is also way more expensive than the clones that you will find on Aliexpress, eBay, or similar stores, will make your life easier. I'm not saying you HAVE to use it, but it's definitely recommended. It is rare, but not impossible, that you will have a chip that will require a different clip, statistically it will be [placeholder], aside from buying a clip that is compatible with your chip the rest of the process is virtually the same.

   [TO BE MOVED] Clip size: Most T400s will require a SOIC 16 or SOIC 8 depending on the chip size. If your T400 is already disassembled, you can just look at the pins of the clip; a 16-pin chip will require a SOIC 16, and an 8-pin chip will require a SOIC 8. If your T400 is not disassembled yet, you can read the chip with the flashrom package and know, based on the memory size of the chip, what clip you will need: an 8mb chip will correspond to a 16 pins chip and a 4mb chip will correspond to an 8 pins chip.

3. Jumper cables: Standard jumper cables are fine; have an assortment of female-male, female-female ready depending on what the interface of your programmer and clip will need. Probably won't need male-male jumpers.

4. Disassembly: You will need to disassemble the T400 for the first flashing of libreboot, once it is installed every next flash of the bios can happen internally. You have two options when it comes to disassembly: you can completely disassemble every single component of the pc, including detaching the motherboard from the plastic cage; or you can just remove the battery and palm rest and "mod" (AKA break) the plastic cage to have access to the chip.

   [PHOTOS]

   Why do I illustrate these two options? Because, in case you just want to libreboot the laptop without doing any additional mods then the less invasive method will save you time and energy, but if you plan to mod further the laptop you can do everything in a single go and disassemble it once (hopefully) The only other mod that will be illustrated in this guide will be the quad-core mod, that allows installing a range of quad-core CPUs on a T400 that would otherwise only have dual-core CPUs compatible. For the cooling mod, that makes sense only after you do the quad-core mod, follow this guide: [LINK]

5. Flashrom installation: If you're using a raspberry as a programmer, ssh into it to install the flashrom package, if you're using the CH341A install the package on the pc you will be connection the programmer to. The package comes with the "flashrom" command, in most cases, this is all you will need to use (we will see common (and less common) flashing errors and their workarounds.

6. Flashrom reading: TODO

## Clip -> chip connection

After having disassembled the device, you will have access, just on top of the two RAM slots, to the bios chip. Using the jumper cables connect your programmer of choice to the Clip and then the clip to the chip. REMEMBER to turn on the programmer only AFTER a solid connection between the clip and chip is established, to avoid any kind of voltage issue. Similarly, turn off the programmer BEFORE removing the clip.

the next step is to read and save the current BIOS, so that, in case anything goes wrong while writing onto the chip, you will have a backup to use to go back to a working BIOS. It is highly recommended to backup the .bin a couple of times and use the command "diff" to check the you have two exact copies of the BIOS, keep trying untill you do. This is the safest option, i never do it cause it bothers me trying to have a working BIOS.
