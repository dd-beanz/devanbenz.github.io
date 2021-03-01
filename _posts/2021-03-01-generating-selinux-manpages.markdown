---
layout: post
title: "Generating SELinux manpages"
date: 2021-03-01 10:45:00 -0600
categories: linux, selinux
---
SELinux does not come with manpages by default.
To install sepolicycoreutils-devel with RHEL/CentOS:

{% highlight bash %}
yum install sepolicycoreutils-devel
{% endhighlight %}

After installing the sepolicy commands, install all (-a) manpages to path (-p) /usr/share/man/man8:

{% highlight bash %}
sepolicy manpage -a -p /usr/share/man/man8
{% endhighlight %}

And thats it! You can now use {% highlight bash %}man -k _selinux{% endhighlight %} to see what selinux man pages are 
available. Generally these man pages will give context information about different selinux policy for services/daemons/processes. 

For more information on SELinux I suggest checking out the man page or [SELinux][selinux] tutorial on linode.

[selinux]: https://www.linode.com/docs/guides/a-beginners-guide-to-selinux-on-centos-8/