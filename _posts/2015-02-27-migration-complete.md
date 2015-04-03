---
layout: post
title:  Migration to Jekyll
date:   2015-03-03 12:00:00
categories: hacks
comments: true
---

# My notes

Migration complete from [Wordpress](https://wordpress.org) to
[Jekyll](http://jekyllrb.com)! Wordpress is a great software and I recommend
it to anyone who needs a complex portal with an easy-to-use interface.
However, I do not have much time to deal with self-hosted Wordpress server
anymore, so I migrated to Jekyll.
The [Github](https://github.com) provides a free repository for hosting static
websites using Jekyll. The service is named
[Github-Pages](https://pages.github.com), and I strongly
recommend it for whom wants a free hosting blog, with the possibility to use a
custom domain name and, after all, being provided by Github.

# Fine tunning

To separate the main page into categories, I used the following code that I figured out by myself.
If you need help to understand this code, you may write a message in the comments.

{% highlight html %}
<div class="blog_main">
  <ul class="post-list">

    {% for category in site.categories %}

      <h1><a name="{{ category[0] }}">{{ category[0] }}</a></h1>

      {% for post in category[1] %}
        <li>
          <h3>
            <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
          </h3>
        </li>
      {% endfor %}

    {% endfor %}
  </ul>
</div>
{% endhighlight %}

# Original migration welcome message

You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve --watch`, which launches a web server and auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll’s dedicated Help repository][jekyll-help].

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

+
