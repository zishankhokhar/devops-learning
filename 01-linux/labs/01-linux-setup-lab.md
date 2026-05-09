# Linux Setup Lab

## System Information
- OS: Ubuntu 22.04 LTS
- VM: UTM on macOS
- Specs: 4 CPU cores, 4GB RAM, 40GB storage
- Install Method: Virtualization using Ubuntu ISO

# Steps I Completed
- Installed UTM on macOS
- Created a Linux VM using Virtualize → Linux
- Attached Ubuntu ISO and configured CPU/RAM/storage
- Installed Ubuntu Server with default settings
- Removed ISO and rebooted into terminal
- Installed Ubuntu Desktop GUI
- Logged into the full Ubuntu interface and opened the terminal

## Commands I Ran
```bash
sudo apt update
sudo apt install ubuntu-desktop

## What I learned
- How to set up a Linux VM using UTM
- Difference between virtualization and emulation
- Installing a GUI on top of Ubuntu Server
- Using sudo and apt for package management

## Issues I faced
- Had to remove ISO to stop reinstalling loop
- Mouse not usable during server installation (keyboard only) 