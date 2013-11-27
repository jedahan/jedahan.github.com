---
layout: post
title: How to get opencv 2.4.7 and openFrameworks 0.8.0 to play nicely with OSX 10.9
---

Make sure you have homebrew

  * brew install python
  * pip install numpy (brew install numpy is not enough)
  * add the following to args in /usr/local/Cellar/Formula/opencv.rb:
    * -DCMAKE_OSX_SYSROOT='/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.8.sdk/'
    * -DCMAKE_OSX_DEPLOYMENT_TARGET=10.8
    * -DOPENCV_EXTRA_C_FLAGS='-mmacosx-version-min=10.8'
    * -DOPENCV_EXTRA_CXX_FLAGS='-mmacosx-version-min=10.8'
  * npm install opencv
  * use [nick hardeman's 64-bit fork of openFrameworks](https://github.com/NickHardeman/openframeworks_osx_64)
  * make sure all the targets are 10.8 for your app
  * add the correct dylibs from /usr/local/lib to the project

  I should post a sample project sometime, so its a little less obscure reading these notes.