---
layout: post
title: Pop!_OS - Terminator Terminal Emulator
description: >
  Switching the default terminal emulator on Pop!_OS 22.04 to Terminator.
categories: [kbase]
tags:       [pop!_os, linux, sysops]
---
1. this ordered seed list will be replaced by the toc
{:toc}

## Purpose
The following post documents the process to switch from the default GNOME Terminal application to Terminator on Pop!_OS 22.04.  
More information about Terminator can be found at <https://gnome-terminator.org/>{:target="_blank"}

## Assumptions
A number of assumptions have been made when compiling the below procedure. They include:
+ Basic familiarity with Linux and the terminal.
+ The user account to perform this procedure has **sudo** privileges.
+ While the procedure may work on other versions or Debian derivatives, it has only been tested with **Pop!_OS 22.04**.
+ Terminator should open for all shell activities, including from within other applications.
+ Terminator has not yet been installed.

## Procedure
Steps required to switch to Terminator on a fresh Pop!_OS installation are:
1. Open the existing GNOME terminal (*Super + T*).

2. Update the package manager:  
```shell
apt update
```
3. Install Terminator:  
```shell
sudo apt install terminator
```
4. Set Terminator as the default application from within GNOME:  
```shell
gsettings set org.gnome.desktop.default-applications.terminal exec /usr/bin/terminator  
gsettings set org.gnome.desktop.default-applications.terminal exec-arg "-x"
```
5. *(Optional)* If using the Nemo File Manager, set the default application in cinnamon to Terminator.  
This will ensure that Terminator is opened when using the *Right Click > Open in Terminal* option from within the file manager:  
```shell
gsettings set org.cinnamon.desktop.default-applications.terminal exec /usr/bin/terminator
gsettings set org.cinnamon.desktop.default-applications.terminal exec-arg "-x"
```
6. Log out/in or restart for the changes to take effect.

## Conclusion
After following the procedure above, Terminator should be the default terminal emulator for all shell activities in Pop!_OS 22.04.