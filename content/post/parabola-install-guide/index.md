---
title: Parabola Installation Guide
description: A recap of the commands needed to have an encrypted, openRC Parabola setup.
date: 2024-02-08 00:00:00+0000
image: parabola.jpg
weight: 2
categories:
      - Linux
      - Libreboot
tags:
      - linux
      - parabola
      - systemd
---

This is a guide on how to install parabola that i created to have a reference for my eventual future installations on a librebooted system.
I decided to write this because I found that following the original guide in the Parabola wiki was not sufficient if you want to have an encrypted disk and no systemd in your system.
Still, this is to be considered just a recap of what you will need to to if you want to install Parabola this way, do not consider this official (or even unofficial) documentation at all.

some info on [Parabola GNU/Linux-libre](https://www.parabola.nu/)

I will assume that you already created a bootable drive of some kind with an image of Parabola CLI Edition that you can download from here: [download](https://wiki.parabola.nu/Get_Parabola)\
I won't cover how to do so because there are already hundreds of guides that perfectly teach you how to do it on every system with every image using every technique available.

## Check if you have a UEFI machine or not
Type the following command to check if you have a UEFI machine or not, and keep that in mind, we will use this information later
```
ls /sys/firmware/efi/efivars
```
## Format your drive
The choice of partitions and filesystems is a matter of preference, and beyond the scope of this install guide. You can look at the Parabola wiki to know more.
If you already know what do you want and how you want it, you can skip this part.

Proceed to format the drive you be installing Parabola on. I use fdisk, the most basic things you need to know about it are:
type **d** to delete a partition (will ask number), type **n** to create a partition (will ask usual info), type **w** to confirm the changes.

Lets target the drive:
```
fdisk /dev/sdX
```
Assuming you deleted any existing partition, the next is to create two partitions, the first one will be a 1Gb partition and the second one will be the rest of the disk (or anyhow how much space yo want on your system)
This is just the way i do it, you might find your needs are different.

```
Command (m for help): n
Partition type
   p   primary (0 primary, 0 extended, 4 free)
   e   extended (container for logical partitions)
Select (default p):

Using default response p.
Partition number (1-4, default 1):
First sector (2048-30277631, default 2048):
Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-30277631, default 30277631): +1G

Created a new partition 1 of type 'Linux' and of size 1 GiB.
```

Then we are gonna create the second partition, you can press enter and use the default values for every option, you will have something similar to this:

```
Command (m for help): n
Partition type
   p   primary (0 primary, 0 extended, 4 free)
   e   extended (container for logical partitions)
Select (default p):

Using default response p.
Partition number (1-4, default 1):
First sector (2048-30277631, default 2048):
Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-30277631, default 30277631):

Created a new partition 1 of type 'Linux' and of size X.XX GiB.
```
Modify the last sector if you need a specific amount of memory or leave it blank to take the entire free space of your drive.
It might ask you to remote an already present signature, in that case just remote it by pressing **Y** when asked to.

## Filesystem of boot partition

We are now gonna put a filesystem on the first partition, I use FAT partitioning because it is versatile since it's compatible with both legacy boot and UEFI.
```
mkfs.fat -F32 /dev/sdX1
```

## Encrypt the second partition
To encrypt out partition we run the command:
```
cryptsetup luksFormat /dev/sdX2
```
You be ask to confirm the choice by typing **YES** and you will be asked to insert the passphrase for the partition.

## Decrypt sdX2
```
cryptsetup open /dev/sdX2 partition-name
```
We now decrypt the partition and assign a name to it (the name can be a random string, it will change later anyhow)
If we now run ```lsblk``` we should see something like this:
```
NAME                MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINTS
nvme0n1             259:0    0 476.9G  0 disk
├─nvme0n1p1         259:1    0     1G  0 part  
└─nvme0n1p2         259:2    0 475.9G  0 part
  └─partition-name  254:0    0 475.9G  0 crypt 
```

## Create filesystem for partition-name
Create a [btrfs](https://wiki.archlinux.org/title/btrfs) partition on the decrypted partition
```
mkfs.btrfs dev/mapper/partition-name
```

## Mount both partition
Mount the two partitions starting with partition-name:
```
mount /dev/mapper/partition-name /mnt
```
Then create a directory called **boot**:
```
mkdir /mnt/boot
```
And then mount the boot partition in the boot folder:
```
mount /dev/sdX1 /mnt/boot
```
If you now run ```lsblk``` again you should see the partition correctly mounted:
```
NAME                MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINTS
nvme0n1             259:0    0 476.9G  0 disk
├─nvme0n1p1         259:1    0     1G  0 part  /mnt/boot
└─nvme0n1p2         259:2    0 475.9G  0 part
  └─partition-name  254:0    0 475.9G  0 crypt /mnt
```
## (optional) Change mirrors
You might want to change the mirrors order to make installation of packages faster by going into this file (use your favorite text editor):
```
/etc/pacman.d/mirrorlist
```
From the list, move the servers that are closer to you to the top so that they will be the first ones to be chosen.

## Install packages into the system
Install the needed packages into the ```/mnt``` partition, add what you know you will need:
```
pacstrap /mnt base base-devel linux-libre linux-libre-firmware btrfs-progs grub networkmanager cryptsetup lvm2 vim neovim
```
If you're in UEFI then add the following package: ```efibootmgr```

- base and base-devel:\
base is the basic system and all the tools related to it, base-devel is necessary to compile packages and other stuff
- linux-libre:\
the libre version of the linux kernel, with no binary blobs, obfuscated code, or code released under proprietary licenses
- linux-libre-firmware:\
Some hardware devices such as the popular NetGear WNA1100 (aka: Wireless-N 150, aka: Atheros AR9271) require firmware (eg: ath9k_htc) from the linux-libre-firmware package
- grub:\
the boot loader
- networkmanager:\
internet 'n stuff
- cryptsetup and lvm2:\
packages needed for encrypting and decrypting the drive
- vim and neovim:\
i mean you know why

## Chroot into your system
```
arch-chroot /mnt bash
```

## Set the timezone and set the hardware clock
just run:
```
ln -s /usr/share/zoneinfo/Europe/Rome /etc/localtime
```

Change country and city based on your correct timezone
Then synch the hardware clock with the system clock:
```
hwclock --systhoc
```

## Setup keyboard layout and language
Edit the locale.gen file:
```
nvim /etc/locale.gen
```
Uncomment the your language and layout of choice

Edit the file locale.conf:
```
nvim /etc/locale.conf
```
I will add the setup for the US keyboard but you might want a different layout:
```
export LANG="en_US.UTF-8"
export LC_COLLATE="C"
```
Run the locale-gen command:
```
locale-gen
```
## Name your computer
Run:
```
echo "myhostname" > /etc/hostname
```

change **myhostname** with your desired name, then edit the following file:
```
nvim /etc/hosts
```
and add the following lines:
```
127.0.0.1   localhost
::1         localhost
127.0.1.1   myhostname.localdomain myhostname
```

## Enable NetworkManager service
run:
```
systemctl enable NetworkManager.service
```

## Add a user and set his groups and password
First add a password to your root with:
```
passwd
```
Then create a new user:
```
useradd -G wheel -m user
```
this way a user by the name of **user** has been created, added to the wheel group and a home directory has been created for him
Set the user user password:
```
passwd user
```

## Edit the mkinitcpio configuration
Edit the **mkinitcpio.conf** file:
```
nvim /etc/mkinitcpio.conf
```
look for the line in which hooks are declared, it is going be like this:
```
HOOKS=(base udev autodetect modconf kms keyboard keymap consolefont block filesystem fsck)
```
add to the hooks **encrypt** and **lvm2**:
```
HOOKS=(base udev autodetect modconf kms keyboard keymap consolefont block encrypt lvm2 filesystem fsck)
```
**Optionally** you can add the following modules to same mkinitcpio.conf file:
```
hid usbhid hid_generic ohci_pci
```
If, at the end of the installation, the keyboard is not working during the decryption of the partition\

Update the conf by typing:
```
mkinitcpio -p linux-libre
```

## Make the system able to decrypt the partition
Start by exiting the partition:
```
exit
```
Create an fstab and output it in the correct place:
```
# genfstab -p /mnt >> /mnt/etc/fstab
```
use **-U** or **-L** to define by UUID or labels, respectively

Take the output of **lsblk -f** in put it in the following file:
```
lsblk -f >> /mnt/etc/default/grub
```
Go back into your system:
```
arch-chroot /mnt bash
```

## Edit GRUB to make the system able to encrypt and decrypt the partition
Enter the following file:
```
nvim /etc/default/grub
```
At the end of the file you will find the output of our **lsblk -f** command, it will be something similar to this:
```
NAME         FSTYPE FSVER LABEL UUID FSAVAIL FSUSE% MOUNTPOINTS
sdb
nvme0n1
├─nvme0n1p1                     [UUID_0]      862.4M    16% /boot
└─nvme0n1p2                     [UUID_1]
  └─cryptlvm                    [UUID_2]      431.2G     9% /
```
You will only need the two UUIDs: **[UUID_1]** and **[UUID_2]**


And at the top of this file there will be a line that looks like this:
```
GRUB_CMDLINE_LINUX_DEFAULT="loglevel=3 quiet" 
```
Now, take the UUID of the encrypted partition (in this case the **UUID_1**) and add the following to the GRUB_CMDLINE_LINUX_DEFAULT:
```
cryptdevice=UUID=[UUID_1]:cryptlvm
```
It will look something like this:
```
cryptdevice=UUID=33dd1b52-a543-4143-8bf8-004390e411e0:cryptlvm
```
Take the UUID of the decrypted partition (in this case the **UUID_2**) and add the following to the GRUB_CMDLINE_LINUX_DEFAULT:
```
root=UUID=[UUID_2]
```
It will look something like this:
```
root=UUID=b720a64e-fdf2-462e-9231-d1a35ae2654e
```
the **GRUB_CMDLINE_LINUX_DEFAULT** should look like this:
```
GRUB_CMDLINE_LINUX_DEFAULT="loglevel=3 quiet cryptdevice=UUID=33dd1b52-a543-4143-8bf8-004390e411e0:cryptlvm root=UUID=b720a64e-fdf2-462e-9231-d1a35ae2654e" 
```

## Install Grub bootloader
Install GRUB for UEFI devices:

**esp** denotes the mountpoint of the EFI system partition
```
grub-install --target=x86_64-efi --efi-directory=[esp] --bootloader-id=grub
```

Install GRUB for legacy BIOS devices
```
grub-install /dev/sdX
```
Then create the grub configuration:
```
grub-mkconfig -o /boot/grub/grub.cfg
```

Now you can unmount your partitions, remove your bootable device and reboot the system.
You now a have a fully libre system, you chad.

## Migrate to Open-RC
For maximum chad-status you have to remote systemD in favour of Open-RC, the Parabola wiki has a section on how to do so [HERE](https://wiki.parabola.nu/OpenRC)

First, upgrade your currently installed packages from your currently configured repositories: 
```
pacman -Syyuu
```
Then, add the following lines in /etc/pacman.conf:
```
[nonsystemd]
Include = /etc/pacman.d/mirrorlist

# Enable [nonsystemd-multilib] only if you have [multilib] enabled
#[nonsystemd-multilib]
#Include = /etc/pacman.d/mirrorlist
```
Next, replace your currently installed packages with those from the [nonsystem] repo. 
```
pacman -Syyuu
```
