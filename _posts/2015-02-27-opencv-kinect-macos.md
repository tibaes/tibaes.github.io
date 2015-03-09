---
layout: post
title:  "OpenCV Kinect MacOS Brew +"
date:   2015-02-27 11:32:00
categories: hacks
---
# Installation
To install OpenCV v2.4.9 with OpenNI support, first you need to install Apple XCode Command Line Tools, Java and Java SDK. Then you can use the following brew commands:

{% highlight bash %}
brew tap homebrew/science
brew tap totakke/openni
brew install openni
brew install sensor-kinect
brew install nite
brew install --with-cuda --with-ffmpeg --with-openni --with-tbb opencv
{% endhighlight %}

Choose the desired flags, in this case the Nvidia CUDA, FFMpeg, OpenNI and Intel TBB were active. When using TBB, sometimes the **pkg-config** needs to be fixed by changing the **-llibtbb.dylib** to **/usr/local/lib/libtbb.dylib** in the file _/usr/local/lib/pkgconfig/opencv.pc_

Install also libfreenect, so you can use commands like freenect-glview
{% highlight bash %}
brew install libfreenect
{% endhighlight %}

Obs. Apple XCode Command Line Tools can be installed using:
{% highlight bash %}
xcode-select --install
{% endhighlight %}

# Usage
To compile some OpenCV code, probably you need to use **libstdc++** (GNU C++) instead of **libc++** (LLVM). See an example of the compilation command line:

{% highlight bash %}
g++ -stdlib=libstdc++ `pkg-config --cflags opencv` simpleflow.cpp `pkg-config --libs opencv` -o simpleflow
{% endhighlight %}

It is more elegant to use a Makefile, as the one bellow:
{% highlight make %}
SHELL := /bin/bash
CFLAGS=-Wall -Wno-overloaded-virtual -stdlib=libstdc++ -O2 `pkg-config --cflags opencv`
CXXFLAGS=$(CFLAGS)
LDFLAGS=`pkg-config --libs opencv`
{% endhighlight %}

Notice that the first line just tells the Makefile the correct shell environment to use with make. This fix compatibility issues when you use an alternative shell – I use and recommend the [fishshell](http://fishshell.com).

+
