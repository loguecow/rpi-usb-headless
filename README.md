# Raspberry Pi USB Headless Setup

This guide explains how to set up a Raspberry Pi for headless operation over USB, enabling SSH access without the need for an external monitor, keyboard, or network connection.

## Prerequisites
- A Raspberry Pi (Zero, Zero W, or other models supporting USB gadget mode)
- A microSD card with Raspberry Pi OS installed
- A computer with an available USB port

## Steps to Configure Headless USB Access

### 1. Modify `cmdline.txt`
Edit the boot configuration file on the SD card:
```sh
sudo nano /boot/cmdline.txt
```
Add the following before `rootwait`:
```
modules-load=dwc2,g_ether
```
Save and exit.

### 2. Modify `config.txt`
Edit the Raspberry Pi configuration file:
```sh
sudo nano /boot/config.txt
```
Add the following line at the end:
```
dtoverlay=dwc2,dr_mode=peripheral
```
Save and exit.

### 3. Configure Network Interface
Edit the network interfaces file:
```sh
sudo nano /etc/network/interfaces
```
Add the following:
```
allow-hotplug usb0
iface usb0 inet static
    address 192.168.7.2
    netmask 255.255.255.0
    network 192.168.7.0
    broadcast 192.168.7.255
    gateway 192.168.7.1
```
Save and exit.

### 4. Enable SSH
To enable SSH, create an empty file named `ssh` in the `/boot` directory:
```sh
touch /boot/ssh
```

### 5. Connect and Access via SSH
- Connect the Raspberry Pi to your computer using a USB cable.
- Wait for the Pi to boot up.
- SSH into the Raspberry Pi using:
```sh
ssh pi@192.168.7.2
```
(Default password: `raspberry`)

## Troubleshooting
- Ensure your computer recognizes the Raspberry Pi as a network device.
- Try restarting both the Raspberry Pi and your computer.
- Use `ifconfig` or `ip a` to check the USB interface status.

## References
- Raspberry Pi USB Gadget Mode Documentation
- Official Raspberry Pi OS Setup Guide

Enjoy your headless Raspberry Pi setup!

