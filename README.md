quick-lxc-deploy
================

Couple of bash scripts hacked together for quick deploying/accessing LXC containers in new environments.

### Deploying a container

Usage: quick-lxc-deploy &lt;debian version&gt; &lt;architecture&gt; [&lt;container name&gt;]

quick-lxc-deploy takes care of:

* fetching predefined set of packages and packing them into tarball in your CACHE_DIR directory
* installing new container in DEPLOY_DIR directory
* creating SSH key files in ~/.ssh/lxc_rsa for root and current user (for speed-dialing with lxcssh)
* creating an account for current user on a target container with rbind-mounting user's home directory

Configuration file - ~/.quick-lxc-deploy.conf

quick-lxc-deploy uses the following options:

* PACKAGES - additional packages list to be included into container
* MIRROR - mirror's url for debootstrap
* CACHE_DIR - path to directory storing debootstrap's tarballs
* DEPLOY_DIR - prefix path for container rootfs

lxcssh
======

Speed-dial-like access to a container.

### Speed dialing

Typical lxcssh output:

```
[rjeczalik@rjeczalik-ub64 rjeczalik]$ lxcssh
[0] lenny-amd64 (10.0.3.132)
[1] lenny-i386 (10.0.3.166)
[2] squeeze-amd64 (10.0.3.107)
[3] squeeze-i386 (10.0.3.190)
```

lxcssh connects to a container as current user - e.g. in order to login as root to squeeze-amd64 container call sudo lxcssh 2.
