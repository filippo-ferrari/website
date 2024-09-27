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
This is a collection of tools I am using on my M1 Macbook Pro. Most of it is still a work in progress.

I am using the Yabai tiling window manager and skhd as hotkey daemon to replicate the setup I have on my Linux machines as much as i can, Alacritty as my terminal emulator, Powerlever10k as zsh theme and more.
I also made a number of changes in the system setting to remove most of the annoying and/or useless macOS features.

## System settings
### Desktop & Dock
- Set **Click wallpaper to reveal desktop** to **Only in Stage Manager**
- Uncheck **Show items On Desktop**
- Remove all apps from the dock
- Set dock size to as small as possible
- Check **Automatically hide the Dock**
- Uncheck **Animate opening applications**
- Uncheck **Show suggested and recent apps in the Dock**
- Disable Widget completely 
### Notifications
- Disable all notifications when the screen is on and unlocked
- Keep notifications when screen is on and locked
### Control Center
- Remove everything except Clock, WiFi and Battery indicators
- More changes will be done during the Menu Bar setup
### Siri & Spotlight
Completely disable Siri, leave Spotlight unchanged, won't be using it anyway once RayCast is installed
## RayCast
I use RayCast as an app launcher, although it can do way more things than just launch your apps, and if you're interested you can check the enormous amount of community plugins available.

Download and install [RayCast](https://www.raycast.com/), follow the tutorial if necessary.
- Disable **Window Manager** control

## Homebrew
A package manager for MacOS. Does what it's supposed to do, most of the times.\
Can be installed as a RayCast plugin and used by opening RayCast and typing **brew**, but personally i find myself using it from the terminal almost always.
- Download and install [Homebrew](https://brew.sh/)

PS: I still have not looked but know there are (apparently) alternatives, in particular: MacPorts and pkgsrc.

## Hidden Bar
Install Hidden Bar using Brew, it's an app that allows you to decide which icons you want to see and which icons you want to hide in your menu bar.\
You will want to start this app at login.

## Stats
[Stats](https://github.com/exelban/stats) is an app for the Menu Bar that shows statistics about the hardware. CPU/GPU/RAM temps and usage, stuff like that.\
I keep only the CPU temp and RAM usage in the bar and hid the rest using Hidden Bar.
You can install Stats using RayCast's plugins or using Homebrew: `brew install --cask stats`

## Alacritty

## Oh My Zsh

## Yabai

## Powerlever10k

## Skhd
