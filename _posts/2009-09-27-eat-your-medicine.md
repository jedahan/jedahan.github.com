---
layout: post
uuid: 7d55a1ec-c52c-4dc5-a8af-dddcc14a843e
title: eat your medicine
---

In a stronger effort to give applications the trial they deserve, I have
uninstalled my old standbys.

    paludis --uninstall vim; paludis --install diakonos gedit

I am looking for something between nano and vim with the suckless philosophy
  * good: consistent keybindings for most of my apps
  *  bad: feel less productive, especially missing 'cw' and 'dw'
  * ugly: missing exheres-syntax.vim

    paludis --uninstall firefox; paludis --install chromium-bin

This was a much easier switch.
  * good: blazingly fast
  * more good: don't miss any firefox features
  * good,good: greasemonkey scripts, google bookmarks integration
  * amazing: flash doesn't stutter or crash!

The *only* problem was nss reporting all certificates as revoked, but that was a
clock issue, fixed with the following commands:

    echo "TZ=\"America\/New_York\" >> /etc/env.d/00basic
    sudo eclectic env update
    ntpdate tick.stonybrook.edu
    hwclock --systohc # dual boot with bad OS means clock is set to local

It was actually chromium's strictness denying access to sites with revoked
certificates that forced me to fix my clock. FYI firefox doesn't have this bug
because they work around it.
