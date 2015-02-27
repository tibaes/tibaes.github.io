---
layout: post
title:  "Hacking the GoPro network"
date:   2015-02-27 17:26:00
categories: developer network
---
If you want to send commands to the GoPro camera without using the official app,
 here are some tips that may help you. First, connect the device
 (computer, tablet or smartphone) into the GoPro wifi; then use the commands
 bellow. In my case, the commands followed this pattern:

{% highlight bash %}
http://10.5.5.9/bacpac/<command>?t=<key>&p=<command-option>
{% endhighlight %}

Suppose that the network key is “boo”, so to capture an image:

{% highlight bash %}
http://10.5.5.9/bacpac/SH?t=boo&p=%01
{% endhighlight %}

Now, to turn the camera on and off, respectively:

{% highlight bash %}
http://10.5.5.9/bacpac/PW?t=boo&p=%01
http://10.5.5.9/bacpac/PW?t=boo&p=%00
{% endhighlight %}

The navigation through photos and videos uses the port *8080*:

{% highlight bash %}
http://10.5.5.9:8080/
{% endhighlight %}

# Discover by yourself
But if you want to get the commands for yourself, you just need to sniffer
the network while sending commands to the camera using the official
app.

You need to know the iOS UDID to sniffer an iOS device, which is explained
[here](http://whatsmyudid.com).
Now, with your device plugged into an USB port and connected in the GoPro's
wifi, use these commands bellow.

{% highlight bash %}
rvictl -s <UDID>
ifconfig rvi0
sudo tcpdump -n -t -A 0 -i rvi0 -w dump.pcap
{% endhighlight %}

The first command sets the iOS as a virtual interface. Then we use this
interface and start dumping. Now you should use the official app to send
the desired commands to the camera. All the commands will be in the dump.pcap
file, following the same pattern as mentioned above. The last thing to do is
to shut down the virtual interface when you are done.

{% highlight bash %}
rvictl -x <UDID>
{% endhighlight %}

+
