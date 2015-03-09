---
layout: post
title:  "Remote Gitlab through SSH"
date:   2015-02-27 11:32:00
categories: hacks
---

# Terminal
Use the instructions bellow to get remote access to a local gitlab server
protected by a firewall. Requires ssh access, of course.
To use just the git features on terminal, first you need to make a bridge,
so open a terminal and use the command below.
High port can’t be a reserved port, or one already in use.

{% highlight bash %}
ssh -L <high port>:<gitlab server>:22 <remote server>
{% endhighlight %}

Example using local port *3333* to access the gitlab server,
which has the address *192.168.1.10* inside the *firewall.ufpr.br* network.
The target port in the gitlab server is the usual *22*, default for ssh.

{% highlight bash %}
ssh -L 3333:192.168.1.10:22 firewall.ufpr.br
{% endhighlight %}

Next, open another terminal to run the git commands you desire.
The trick is to access a localhost server at the chosen port.
Just the *git clone* must take care if the unusual process.
Subsequent *push*, *pull*, *add*, *commit* does not any special typing.
However, the ssh tunnel must be opened to perform any *push* or *pull*.

{% highlight bash %}
git clone ssh://git@localhost:3333/project.git
{% endhighlight %}

# Browser
If you need to access the web interface of git lab, you do not need the above instructions. All you need is a basic ssh proxy, as:

{% highlight bash %}
ssh -D <high port> <remote server>
{% endhighlight %}

Example
{% highlight bash %}
ssh -D 4444 firewall.ufpr.br
{% endhighlight %}

Next, set your web browser to use socks proxy at localhost and the chosen port,
an example is presented in Figure 1.
Then, go to the local address of the gitlab server, *192.168.1.10*
 in our example.

<figure>
<img class="large-img" src="/assets/posts/firefox-proxy.png">
<figurecaption>
  Figure 1: Screenshot of my firefox proxy settings.
</figurecaption>
</figure>

+
