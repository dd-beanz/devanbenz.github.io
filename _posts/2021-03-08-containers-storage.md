---
layout: post
title: "Attaching host storage to podman containers"
date: 2021-03-08 22:25:00 -0600
categories: linux, podman, containers
---
There are plenty of times when running a podman container will require binding a location on the host machine to a location within the container.
When I add storage to a container I usually do it in the following method:
- Create the Directory  
`sudo mkdir /hostdir`
- Give ownership of the directory to account that will start the container
`sudo chown podmanaccount:podmanaccount /hostdir`
- Set the SELinux context type to container_file_t and restore labeling to add new context
`sudo semanage fcontext -a -t container_file_t "/hostdir(/.*)?" && restorecon -R /hostdir`
- Now when running the container you need to indicate storage binding with option `-v` (nginx example)
`podman run -n webserver -v /hostdir:/usr/share/nginx:Z -d -p 8000:80 nginx`

Now you have persistent storage attached! Remember, this storage will only last the life of the container.
For more info on podman check out the [docs][docs]

[docs]: http://docs.podman.io/en/latest/