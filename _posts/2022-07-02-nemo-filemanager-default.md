---
layout: post
title: Pop!_OS - Nemo File Manager
description: >
  Switching the default file manager on Pop!_OS 22.04 to Nemo.
sitemap: false
hide_last_modified: false
---
# Pop!_OS - Nemo File Manager

## Purpose
The following post documents the process to switch from the default GNOME Files (Nautilus) application to Nemo on Pop!_OS 22.04.

## Assumptions
A number of assumptions have been made when compiling the below procedure. They include:
+ Basic familiarity with Linux and the terminal.
+ The user account to perform this procedure has **sudo** privileges.
+ While the procedure may work on other versions or Debian derivatives, it has only been tested with **Pop!_OS 22.04**.
+ Nemo should open for all file management activities, including from within other applications.
+ Nemo has not yet been installed.

## Procedure
Steps required to switch to Nemo on a fresh Pop!_OS installation are:
1. Open a terminal (*Super + T*).

2. Update the package manager:  
```
apt update
```
3. Install Nemo:  
```
sudo apt install nemo
```
4. Set Nemo as the default application to handle directories:  
```
xdg-mime default nemo.desktop inode/directory application/x-gnome-saved-search
```
This can be verified by running:  
```
xdg-mime query default inode/directory
```
A successful update will show `nemo.desktop`
5. Update dbus to use Nemo as the default file manager:  
```
mkdir -p ~/.local/share/dbus-1/services
ln -s /usr/share/dbus-1/services/nemo.FileManager1.service ~/.local/share/dbus-1/services/
```
6. Log out/in or restart for the changes to take effect.

## Conclusion
After following the procedure above, Nemo should be the default file manager for all folder activities in Pop!_OS 22.04.