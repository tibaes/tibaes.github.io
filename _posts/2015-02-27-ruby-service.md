---
layout: post
title:  "Ruby one line service"
date:   2015-02-27 17:10:00
categories: developer network
---
You can get a HTTP server using only ruby.
There is no need to setup apache, lighttp or nginx
if you need a server just for a moment.
The command is really simple, you just need to know the root directory
for the web service and a port.
Remember to use a non pretected port, i.e. above 1024.

{% highlight bash %}
ruby -run -e httpd <directory> -p <port>
{% endhighlight %}

Here is an example of a HTTP service for the current directory,
running in the port 9090. Using the browser, you can go to
*http://localhost:9090* and all the files in the directory will be listed.

{% highlight bash %}
ruby -run -e httpd . -p 9090
{% endhighlight %}

Useful, right? +
