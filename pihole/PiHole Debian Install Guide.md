# Pi Hole Network Wide Ad Blocker

Work in Progress

Need to add these to the guide

* SSH config for security
* Pihole install
* Whitelist and Blacklists
* Unbound DNS server
* Custom tweaks
* Pihole log to RAM
* Pihole API brower extensions, mac, and phone apps


https://pi-hole.net/

**NOTE:** We will be using a headless OS, all configuration will be done through a terminal.

This guide covers the installation of Raspberry Pi OS (previously called Raspbian) to your Raspberry Pi (any model). Then the installation of pihole followed by the setup for pihole blocklists and whitelists.

At the end there is an advanced step of installing Unbound on your Pi to run your own DNS server.

Table of Contents
=================

   * [What you need before you start](#what-you-need-before-you-start)
   * [1. Install OS](#1-install-os)
   * [2. Enable SSH](#2-enable-ssh)
   * [3. Initial boot and Router Static IP](#3-initial-boot-and-router-static-ip)
   * [4. Lockdown SSH Access (highly recommended but not required)](#4-lockdown-ssh-accesshighly-recommended-but-not-required)
   * [5. Install PiHole](#5-install-pihole)

## What you need before you start

1. Raspberry Pi (any model)
1. Good power cable
1. Case for the pi is recommended but not required
1. Recommend a 32GB Micro SD card for longetivity, but 8GB is the minimum
1. Ethernet cable to plug it into your router
1. Terminal with SSH, Ex. Ubuntu Terminal on Windows 10, Mac, Linux.

## 1. Install OS

1. Download balenaEtcher - https://www.balena.io/etcher/
1. Download Raspberry Pi OS 32-bit **Lite** - https://www.raspberrypi.org/downloads/raspberry-pi-os/
1. Plug your Micro SD card into your PC
1. Open Etcher and flash the OS to the card
1. OS install is done, keep SD card plugged in for next steps

## 2. Enable SSH
We need to enable SSH access to the OS. During the initial bootup of the OS it will see this file and enable SSH to be accessible from the network.

1. Open your terminal
1. In your terminal run `df -h` to see the mounted volumes. Find your SD card.
1. Change your directory to the mount point of the volume. For example: `cd /my/mountpoint`
1. Create an empty file named `ssh` in the directory. Run this command: `touch ssh`

## 3. Initial boot and Router Static IP

1. Unplug your SD card from your PC and plug it into the pi
1. Connect the ethernet cable from your router to the pi
1. Connect the power cable to your pi
1. Your pi is now booting up, wait about 30 seconds
1. On your PC connect to your Router and go to your DHCP reservations. Find the IP of the pi and use it for the next step
1. From your PC's terminal try to ssh into the pi: `ssh pi@IP_ADDRESS`. If this doesn't work either your pi is still booting or you messed up Stage 2 Enable SSH.
1. In your Router go back to the DHCP Reservations and set a static IP for your pi. Remember this
1. In your terminal you should still be connected to the pi. You need release the old DHCP on the pi. Run these commands: `sudo dhclient -r eth0 && sudo dhclient eth0`
1. To verify this change run: `hostname -I` You should see the new static IP
1. Close the SSH connection, run: `exit`

## 4. Lockdown SSH Access (highly recommended but not required)

SSH is completely open to anyone on the home network. Lets lock it down to only you.

## 5. Install PiHole

1. In your terminal SSH into the pi: `ssh pi@STATIC_IP`
1. Download pihole installer: `wget -O basic-install.sh https://install.pi-hole.net`
1. Install pihole: `sudo bash basic-install.sh`
