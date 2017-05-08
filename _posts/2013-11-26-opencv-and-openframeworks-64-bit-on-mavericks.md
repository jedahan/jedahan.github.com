---
layout: post
title: How to get opencv 2.4.x and openFrameworks 0.8.x to play nicely with OSX 10.9
---

Here is how to build a fully 64-bit openFrameworks application, with the latest OpenCV on OSX 10.9.
We need to modify the build options for homebrew's opencv formula to force linking against the
latest osx library, then tell openFrameworks to do the same.

Make sure you have homebrew installed, then do the following:

  * `brew install python numpy`
  * `pip install numpy`
  * add the following to args in /usr/local/Cellar/Formula/opencv.rb:

        -DCMAKE_OSX_SYSROOT='/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.9.sdk/'
        -DCMAKE_OSX_DEPLOYMENT_TARGET=10.9
        -DOPENCV_EXTRA_C_FLAGS='-mmacosx-version-min=10.9'
        -DOPENCV_EXTRA_CXX_FLAGS='-mmacosx-version-min=10.9'


  * `brew install opencv`
  * use [nick hardeman's 64-bit fork of openFrameworks](https://github.com/NickHardeman/openframeworks_osx_64)
  * make sure all the targets are 10.9 for your app
  * add the correct dylibs from /usr/local/lib to the project
  * If you are using the makefiles, just prepend the following to your project `Makefile`

        USER_CFLAGS = -I/usr/local/include
