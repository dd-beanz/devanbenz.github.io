---
layout: post
title: "Running podman containers as a user service"
date: 2021-03-04 08:11:00 -0600
categories: linux, podman, containers
---
Podman containers are great as they can run rootless/daemon-less. But sometimes you just want a container to run
as an enabled service  - perhaps you have an account that specifically is for managing containers and 
the containers should run as a service. 

Before starting the container as a service user lingering must be setup
{% highlight bash %}
loginctl enable-lingering <user>
{% endhighlight %}
lingering will allow the user account services to remain active even if the user logs off 

The `~/.config/systemd/user` directory is where all user configured systemd files will be located. 
To generate a podman service file:
{% highlight bash %}
podman generate <existing container> --name <name> --files
{% endhighlight %}
If the container does not yet exist you can use `--new` as well to indicate that its a new container - there will 
be further configuration needed within the service unit though. 

After generating the container service files the user service daemon needs to be reload, then the service unit can be 
enabled 

{% highlight bash %}
systemctl --user daemon-reload

systemctl --user enable container-<name>.service
{% endhighlight %}

And thats it! There is now a container service unit that can automatically start when the server boots! 
For more information regarding podman checkout the [podman docs][docs]

[docs]: http://docs.podman.io/en/latest/