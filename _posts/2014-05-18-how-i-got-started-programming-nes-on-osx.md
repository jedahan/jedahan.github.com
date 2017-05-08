---
layout: post
title: How I Got Started Programming NES (on OSX)
---
# How I Got Started Programming NES (on OSX)

## Basic Development Software

   This is stuff any OSX developer should already have up and running - a way to compile code (xcode CLI tools), a package manager for command line applications (homebrew), a package manager for gui applications (homebrew cask), and a virtual machine to develop in (VirtualBox). This only will need to be setup once on each machine and will help a lot for future stuff.

Install Xcode CLI tools if they haven't been already

     pkgutil --pkg-info=com.apple.pkg.CLTools_Executables | grep version || xcode-select --install

Install [homebrew](https://brew.sh) if it isn't there

    brew --version || ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)"

Make sure homembrew is happy, by following all the instructions printed out by

    brew doctor

Install [homebrew cask](https://github.com/phinze/homebrew-cask) to manage gui applications, since homebrew only knows commandline applications

    brew tap phinze/homebrew-cask && brew install brew-cask

Now install VirtualBox - we will be developing and burning in Windows XP because thats where are the good tools are. It is also 100% necessary for burning on EEPROMs, which is the kind of chips NES cartridges use. This install will ask for your password to set permissions.

    brew cask install virtualbox

*Phew!* we now have the basic tools any OSX developer would want on their machine, time for the NES specific stuff!

## NES-Specific Software

Download a copy of IE8-XP virtual image from [Modern IE](http://www.modern.ie/en-us/virtualization-tools/). This is a free, legal, 30-day trial of windows XP 32-bit, which is the most compatable for the ROM burner we are going to use.

## NES-Specific Hardware

The [GQ-4x](http://www.mcumall.com/comersus/store/comersus_viewItem.asp?idProduct=4282) is a great piece of harwdare - it is small, usb powered, and compatable with VirtualBox on OSX, windows XP and windows 7. It's really worth the $90 asking price - there are cheaper tools (~$45) but they seem to be unreliable, some require external power or a serial port and are not compatable with more modern OS' (win7+) like the GQ is. If you do end up getting a different programmer up and running well please let me know so I can add instructions here!

 
