---
title: macOS setup [WORK IN PROGRESS]
description: A description of my current macOS development setup 
date: 2024-09-04 00:00:00+0000
image: macos-setup.png
weight: 999
math: 
license: 
hidden: false
categories:
        - Programming
tags:
        - macos
        - terminal
---
This is a collection of tools I am using on my M1 Macbook Pro. Some of it is still a work in progress.

I am using the Yabai tiling window manager to replicate the setup i have on my Linux machines, Alacritty as my terminal emulator, Powerlever10k as zsh theme and more.
Still, id first start with the changes i made in the system setting to remove most of the annoying and/or useless macOS features.

# System settings
## Desktop & Dock
Set **Click wallpaper to reveal desktop** to **Only in Stage Manager**\
Uncheck **Show items On Desktop**\
Remove all apps from the dock\
Set dock size to as small as possible\
Check **Automatically hide the Dock**\
Uncheck **Animate opening applications**\
Uncheck **Show suggested and recent apps in the Dock**
### Widgets (available since MacOs Sonoma)
Completely disable the widgets
## Notifications
Disable all notifications when the screen is on and unlocked\
Keep notifications when screen is on and locked
## Control Center
Remove everything except Clock, WiFi and Battery indicators\
More changes will be done during the Menu Bar setup
## Siri & Spotlight
Completely disable Siri, leave Spotlight unchanged, won't be using it anyway once RayCast is installed
# RayCast
I use RayCast as an app launcher, although it can do way more things than just launch your apps, and if you're interested you can check the enormous amount of community plugins available.

Download and install [RayCast](https://www.raycast.com/), follo the tutorial if necessary.\
Disable **Window Manager** control
# Homebrew
A package manager for MacOS. Does what it's supposed to do, and you basically have no alterative.\
Can be installed as a RayCast plugin and used by opening RayCast and typing **brew**, but personally i find myself using it from the terminal almost always.
Download and install [Homebrew](https://brew.sh/)
