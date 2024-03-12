---
title: My linux userspace
description: A collection of tools i use in my workflow
image: linux.png
date: 2023-09-07 00:00:00+0000
categories:
        - Linux
        - Programming
tags:
        - linux
        - arch
        - suckless
        - terminal
---
This is a simple collection of all the main tools that i have installed on my system. I do not consider the setup complete yet, but i have already collected enough pieces of software that justify start keeping track of them.

I make heavy use of [Luke Smith](https://github.com/LukeSmithxyz)'s LARBS, a script that i recently forked and changed to better suit my needs.

You can find my version of LARBS [here](https://github.com/filippo-ferrari/LARBS). In an ideal future, there will be a changelog with all the changes that i did from the base(d) version.

## Why Arch Linux?
I don't have enough time to compile Gentoo. 

## Distribution: artix
Artix is basically arch only without that piece of cringeware that is systemd.
When it comes to replacing it you have a number of choices that range from decent to very fucking good, i have only ever used runit but you're free to chose something else of course. 

Visit the [Artix](https://artixlinux.org/) website and check all the neat infos they have:

"Q. Do you hate systemd?
A. No, we don't. In fact, we love systemd. But we would never use [such](https://thehackernews.com/2019/01/linux-systemd-exploit.html) a [sucky piece](https://suckless.org/sucks/systemd/) of [bloatware](https://chiefio.wordpress.com/2016/05/18/systemd-it-keeps-getting-worse/) near [anywhere](without-systemd.org/wiki/index.php/Arguments_against_systemd) we [cared](https://www.theregister.co.uk/2018/10/26/systemd_dhcpv6_rce/) [about](www.softpanorama.org/Commercial_linuxes/Startup_and_shutdown/systemd.shtml) [security](https://www.theregister.com/2019/01/31/systemd_exploit/)"

## Disk encryption: 
In all my devices i encrypt the root partition with a [LUKS](https://en.wikipedia.org/wiki/Linux_Unified_Key_Setup)-formatted partition.

## Window manager: dwm
"[dwm](https://dwm.suckless.org/) is a dynamic window manager for X. It manages windows in tiled, monocle and floating layouts. All of the layouts can be applied dynamically, optimising the environment for the application in use and the task performed.
In tiled layout windows are managed in a master and stacking area. The master area contains the window which currently needs most attention, whereas the stacking area contains all other windows. In monocle layout all windows are maximised to the screen size. In floating layout windows can be resized and moved freely. Dialog windows are always managed floating, regardless of the layout applied."
There is a ton of customization possible and patches that you can compile to modify the behaviour of the window manager, it's very lightweight and runs very well even on my 2008 T400, can't recommend it enough.

## Status bar: dwmblocks
[dwmblocks](https://github.com/torrinfail/dwmblocks) is a modular status bar for dwm written in C, if you run the LARBS script, dwm will arrive with a bunch of very well done scripts for all your general needs.
You can also find pre-made scripts all over the world wide web. It's super minimalistic, super customizable and super light, love it.

## Menu: dmenu
"[dmenu](https://wiki.archlinux.org/title/dmenu) is a fast and lightweight dynamic menu for X. It reads arbitrary text from stdin, and creates a menu with one item for each line. The user can then select an item, through the arrow keys or typing a part of the name, and the line is printed to stdout. dmenu_run is a wrapper that ships with the dmenu distribution that allows its use as an application launcher."
I haven't dabbled particularly with dmenu since it comes with everything you need already outside of the box, it's cool and it supports a ton of stuff, like pass and other shit.

## File manager: lf
[lf](https://github.com/gokcehan/lf) (as in "list files") is a terminal file manager written in Go with a heavy inspiration from ranger file manager. See faq for more information and tutorial for a gentle introduction with screencasts.
super light, super easy to config, and, of course, supports vim bindings

## Email client: neomutt
[neomutt](https://neomutt.org/) is a command line mail reader, has a ton of cool features, its super light and, of course, uses vim bindings.
You can use [mutt-wizard](https://github.com/LukeSmithxyz/mutt-wizard) to easily setup your email accounts. 10+ 

## Battery utility: battop
[battop](https://github.com/svartalf/rust-battop) is an interactive battery viewer written in rust that works from the terminal, it gives you all the basic battery info you want to know using a series of graphs, its very lightweight and supports multiple batteries (if you have a thinkpad you know what im talking about)

## Battery optimization: TLP
[TLP](https://linrunner.de/tlp/index.html) is a feature-rich command line utility for Linux, saving laptop battery power without the need to delve deeper into technical details.
TLP’s default settings are already optimized for battery life and implement Powertop’s recommendations out of the box. So you may just install and forget it.
Nevertheless TLP is highly customizable to fulfill your specific requirements.

P.S. i still can't manage to make the TLP service work properly with runit, so if you want to create a highy customized config you might want to stick to [systemd](https://en.wikipedia.org/wiki/Trash)

## Task manager: htop
Again, if you ever want to be taken into consideration by the cool guys and gals of the ricing sub-scene you have to have this process viewer.
All jokes aside [htop](https://htop.dev/) is a neat piece of software, very light and super useful, written in the mighty C language.

## Text editor: neovim
ok, big boys time, i use vim as my main text editor both to play around in linux and to write code 
i use [AstroVim](https://astronvim.com/) setup, its a very IDE like setup and you can go much more minimalistic if you need to.
That being said i am constantly hopping among major neovim configs so this might very well change in the future.
i didn't customize the setup very much just:
- relative lines set to true
- catcapuccin as my theme
- path_display not truncated
- telescope search with hidden files enabled
- random nerdfont installed using this [guide](https://www.behova.net/install-nerd-font-on-arch-linux/) (i will probably copy it just in case this site cease to exists)
- macro changes
- lazygit 
- other stuff I'm too lazy to remember

Does this setup sucks for your usecase? Remove it with:
```
rm -rf ~/.config/nvim
rm -rf ~/.local/share/nvim
```

## Calendar: calcurse
[calcurse](https://calcurse.org/) is a calendar and scheduling application. Terminal based, has a configurable notification system, uses vim bindings. Cool stuff.

## RSS reader: newsboat
[newsboat](https://newsboat.org) is an RSS/Atom feed reader for the terminal. Super easy to setup and use, uses vim bindings.\
[Here](https://github.com/filippo-ferrari/voidrice/blob/master/.config/newsboat/urls) are the things i follow as of right now.

## Browser: Librewolf
[Librewolf](https://librewolf.net/) is a custom and independent version of Firefox, with the primary goals of privacy, security and user freedom.

## Audio: puslemixer
[Pulsemixer](https://pypi.org/project/pulsemixer/) is a self-sufficient single-file python app that doesn't require any extra libraries. A great CLI mixer.

## Note taking: Logseq
[logseq](https://logseq.com/) is an open-source note taking application that i enjoy using (mainly at work), it supports markdown, tasks management, whiteboards and PDFs annotations.

## Network Manager: nmtui
A text based network interface for NetworkManager, easy to use, configure and modify. 

## Shell history: hiSHtory
[hiSHtory](https://github.com/ddworken/hishtory) stores a history of all your commands, the directory in which you used them, if they succeeded, the time of execution and more. This is stored locally and e2e encrypted.\
You can query them via the ```hishtory``` CLI, it offers a wide range of personalization options and a ton of advanced features like:
- AI shell assistance
- Custom columns
- Web UI
- Filtering duplicate entries
- Syncing

and more. I like it.

## SWAG: neofetch
do i need to say more? you can have it start at login to flex on r/unixporn, normal users will be most likely disgusted (rightfully so)
