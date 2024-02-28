---
title: My Oneplus 6T Linux setup
description: A description of my current Linux phone and its setup
date: 2024-02-23 00:00:00+0000
image: postmarket.png
math: 
license: 
hidden: false
categories:
        - Linux
        - Mobile
        - PostmarketOS
tags:
        - linux
        - postmarketos
        - phosh
---
## <span style="color:black; text-decoration:underline"> Configuration </span>
This is the current configuration i am using while daily driving linux on mobile.\
I am using a [OnePlus 6T](https://www.oneplus.com/it/6t/specs) with [PostmarketOS](https://postmarketos.org/) and the [Phosh](https://phosh.mobi/) user interface.
As a daily driver the phone is basically 100% functional for my use case, your experience may vary depending on your needs.

## <span style="color:black; text-decoration:underline"> Known issues and problems i have experienced </span>

Current issues i have found:
- brightness resets at phone reboot
- default audio output resets at phone reboot
- notch blocking some informations in the top bar (workaround)
- camera not functional
- browser notification not passing through
- gesture to close applications difficult to use
- notifications are not removed when read

## <span style="color:black; text-decoration:underline"> Installation </span>
There are pre-built images of PostmarketOS that can be use if a custom compilation is not needed. The installation of these images if incredibly simple and well documented [here](https://wiki.postmarketos.org/wiki/OnePlus_6_(oneplus-enchilada)).\
Pre-built images can be found [here](https://postmarketos.org/download/).

## <span style="color:black; text-decoration:underline"> Applications </span>
These are the applications that i am currently using/testing:

### <span style="color:green"> Phonecalls </span>
#### Calls
"Calls" is the default application to call used in the OS. As of the writing of this post the app is 100% functional, it can receive and make calls without any issues (at least so far).\
When receiving calls, the vibration and sound work, even when the screen is turned off. Needs some tuning on audio inputs and outputs.

### <span style="color:green"> Messages </span>
#### Chats
"Chats" is the default application to send and receive SMS and MMS messages. I have not tried MMS yet, SMS work perfectly out of the box, no particular setup needed. The app is quite complite and responsive.\
Features include: archiving messages, messages receipts, emojis, seach function and more. Fully functional

### <span style="color:green"> Emails </span>
#### Thunderbird
Thunderbird is very good state overall, i have not needed to look at potential alternatives yet, given how everything i need is in the app already. With a a couple of changes to the view settings it is possible to create a very usable setup.\
Notifications work visually if the app is open in the background, but i have not being able to make the sound of the notifications work.
Once open, emails are fully readable and navigable, they render correctly and have all the standard options available and working (reply, reply list, archive, just, forward, etc).

### <span style="color:green"> Browser </span>
#### Firefox-ESR
The extended support release of Firefox is the default browser of the OS and arrives with **mobile-config-firefox** package already installed, making it usable from the start.\
The browser is fast and responsive, the only issue i have found is that the tabs menu is not working correctly when more tabs than the maximum the view allows are open. I wasn't able to swipe to reach the tabs outside of the view of the menu.\
Aside from that i have found no issue

### <span style="color:green"> Reddit client </span>
#### Giara
Giara is a a Reddit client release under the GPL3 license, written using python and GTK. The app works very well, shows everything the site does, from comments to thumbs up to dates and edits.\
Has the option to copy to the clipboard a comment or post and to open them in the browser. Currently has a slight issue swiping the main page.

#### Headlines
Formely gtkeddit, it is written in C++ and it's an archived project. It's currently still working great, probably slightly faster than Giara, but the UI is older and i don't like the way it manages trees of comments. Still very good as a Reddit client.

### <span style="color:green"> RSS feed </span>
#### Newsboat
Famous RSS/Atom feed reader for the terminal written in C++. Somewhat functional after a couple of easy modifications i have found improved my experience. Instructions will follow.

### <span style="color:green"> Matrix client </span>
#### FluffyChat
Written using flutter, works very well out of the box. Notifications works visually as long as the app is among the open applications tray. Only important piece missing is the ability to play audio messages.\
Requires flatpak installation and flathub repository addition.

#### Fractal
The app works, only the basic functions are there but they are all functional, but i am pretty sure it does not support the e2e chats verification.

#### Nheko
Was not able to login due to a visual bug. I'll wait for a fix and try again, apparently the app is very liked among users.

### <span style="color:green"> WhatsApp </span>
#### WhatsApp Web in Firefox
To have access to WhatsApp chats to talk to normies who don't care about having their conversations be actually private i use the WhatsApp Web interface on Firefox.\
Stuff that works include:
- sending, receiving, reading messages
- reproduce vocal messages
- see media sent and have access to media gallery of chats
- notification sounds when receiving a new message (if browser is open and WhatsApp is a loaded page)
- access to settings

Stuff that dosen't work include:
- visual notification on the phone screen when a message is received (The browser is the one that would need to send that notification)
- sending vocal messages (I was able to give the broser permissions but the issue now relies in the input device, i think)
- making and receiving calls

I have no interest in using features such as: status updates, channels, communities and so on, so i didn't test any of those.

### <span style="color:green"> Phone Camera </span>
#### Megapixels & Millipixels
Not working, no matter what i tried. Still have to look further into it tho. 

### <span style="color:green"> System Process Viewer </span>
#### htop
The famous text based process viewer, honeslty it's here cause its cool. Super cool.

## <span style="color:black; text-decoration:underline"> Some settings i changed (constant Work In Progress tbh): </span>
### Disable vibration during typing
open a terminal and type:
```
gsettings set org.sigxcpu.feedbackd.application:/org/sigxcpu/feedbackd/application/sm-puri-squeekboard/ profile silent
```
### Notch blocking part of the top bar
Following the official PostMarketOS wiki, i edited this file: ```~/.config/gtk-3.0/gtk.css``` with:
```
.phosh-topbar-clock {
  padding-left: 130px;
}
```
### Newsboat changes
To use Newsboat to read RSS feeds (inlcuding the feed of this site!) you can change a couple of things to improve your experience. The default browser used by Newsboat when using the "o" command to open an article in the browser is Lynx.\
Using Lynx in the phone's shell is not impossible but impractical. What i found much better is to pass the Firefox-ESR binary as a variable when launching Newsboat, by editing the **newsboat.desktop** file in ```/usr/share/applications``` like this:
```
[Desktop Entry]
Version=1.0
Name=newsboat

GenericName=RSS/Atom feed reader
Comment=Launches newsboat RSS/Atom feed reader
Keywords=RSS,Atom,News
Categories=Network;ConsoleOnly
X-Purism-FormFactor=Workstation;Mobile;
Type=Application
Icon=newsboat
Terminal=true
Exec=bash -c 'env BROWSER=firefox-esr newsboat %u'
```
This will launch the Firefox-ESR binary and use firefox as the browser. The binary will be executed in the same terminal in which you lanuched the Newsboat binary, so, in order to go back to newsboat, you will need to close Firefox first.

## <span style="color:black; text-decoration:underline"> Basic terminal usage </span>
### Installing a package
```
sudo apk add neofetch
```
### Uninstall a package
```
sudo apk remote neofetch
```
### Seach for a package
```
sudo apk seach neofetch
```
### Upgrade the system
```
sudo akp upgrad -a
```
### Repair packages or a single package
```
sudo apk fix
sudo apt fix neofetch
```
### Manage services
the PostmarketOS service manager is OpenRC, so you can use the ```rc-service``` commands with ease. the command is also symlinked to ```service```, just so you know.
```
 rc-service networkmanager status
 sudo rc-service networkmanager start
 sudo rc-service networkmanager stop
 sudo rc-service networkmanager restart
```
To enable or disable services on boot you can use the ```rc-update``` command
```
# Start NetworkManager on boot (in the default runlevel)
sudo rc-update add networkmanager default

# Stop NetworkManager starting on boot
sudo rc-update del networkmanager default
```
and to see the list of services added to a runlevel you can use ```rc-update```
