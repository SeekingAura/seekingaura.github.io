---
title: WoW Retail - Install
permalink: /docs/gaming_notes/wow_retail/install/
toc: true

previous:
    title: World Of Warcraft Retail (WoW Retail)
    url: "/docs/gaming_notes/wow_retail/"
next:
    title: WoW Retail-First Steps
    url: /docs/gaming_notes/wow_retail/first/
---

Wow is easy to install BUT in case you didn't here i will show you and exlain little bit about files, dirs and update

# Windows Installation
`TODO`


# Linux Installation ?
If for some reason are you don't use windows, don't worry linux community is really big, so there is multiple tools to done a good installation and "virtualization", at the end most of the methods uses [wine](https://www.winehq.org/), however if you are not a Nerd in Computers don't worry, exist other tools that makes this process easy. 

Here i will show in my experience which one works for me, have in mind these steps may differ according to your specific hardware

## Ubuntu 24 Installation

### 1- Graphic Drivers
First we need to install the graphic drivers, according to this [info](https://github.com/lutris/docs/blob/master/InstallingDrivers.md) of Lutris (works for almost any other tool) you could install

For NVIDIA
```shell
sudo dpkg --add-architecture i386 && sudo apt update && sudo apt install -y nvidia-driver-535 libvulkan1 libvulkan1:i386
```

For AMD/INTEL
```shell
sudo dpkg --add-architecture i386 && sudo apt update && sudo apt upgrade && sudo apt install libgl1-mesa-dri:i386 mesa-vulkan-drivers mesa-vulkan-drivers:i386
```
drivers I experimented with Lutris and didn't work for me
### 2- Faugus Launcher
Now install the tool that will help to do all the job [Faugus](https://github.com/Faugus/faugus-launcher), run:

```shell
sudo dpkg --add-architecture i386
sudo add-apt-repository -y ppa:faugus/faugus-launcher
sudo apt update
sudo apt install -y faugus-launcher
```


### 3- Install Battlenet From Faugus-Launcher
Open Faugus launcher, click on "+" located at bottom

IMG

Now click on the drop list with default option *Windows Game* select Battle.net, then ok, **DON'T** modify nothing

IMG

That will setup wine prefix of battlenet, download battlenet installer, then will install, follow the steps until you see the Battlenet Login 


If the installation steps don't open or crash maybe you have the **brwrap issue**
{:.notice-warning}

If you never see the login window on installation process or when you try to open the battlenet from Faugus may you don't have the **expected video drivers** based on your video hardware
{:.notice-warning}


### 3.1- brwrap issue
If you got something like `pressure-vessel-wrap[11882]: E: Child process exited with code 1: bwrap: setting up uid map: Permission denied.`, follow the steps bellow of brwrap issue
{:.notice-warning}

[here](https://github.com/Heroic-Games-Launcher/HeroicGamesLauncher/issues/4102) somone else had the issue and show the solution [here](https://etbe.coker.com.au/2024/04/24/ubuntu-24-04-bubblewrap/), in simple words do this:  


Create text file named bwrap at /etc/apparmor.d/
```shell
sudo nano /etc/apparmor.d/bwrap
```

Then add this

```
abi <abi/4.0>,
include <tunables/global>

profile bwrap /usr/bin/bwrap flags=(unconfined) {
  userns,

  # Site-specific additions and overrides. See local/README for details.
  include if exists <local/bwrap>
}
```

Save and reload apparmor process
```shell
systemctl reload apparmor
```

### 4- Install from battlenet
If everything is ok you will see the battlenet on Faugus, now "play" battlenet

IMG

Login with you Battlenet net app normally then install the wow normally


At this point Any other battlenet game could work
{:.notice-warning}

Once installation ends you can click on play from battlenet and will open wow

IMG

always you will open battlenet from faugus then open wow form battlenet

Could happens every time that you open the wow the resolution changes, but only that
{:.notice-info}


# Optimization

## Recover disk space from old updates

Some data are used for recovery or temporary "fast" updates, but sometimes these files are not eligibles to be deleted "automatically" by battlenet, so based on this [article](https://www.icy-veins.com/wow/news/clear-out-these-wow-folders-and-instantly-free-up-to-50-gb-of-space/) do:

Delete 

C:\Program Files (x86)\World of Warcraft\Data\config
C:\Program Files (x86)\World of Warcraft\Data\indices

These folder are updated to identify the updates and some patch do execute, the issue is that does not delete the old index updates

# References
* https://www.icy-veins.com/wow/news/clear-out-these-wow-folders-and-instantly-free-up-to-50-gb-of-space/