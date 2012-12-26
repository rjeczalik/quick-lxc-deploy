quick-lxc-deploy
================

Couple of bash scripts hacked together for quick deploying/accessing LXC containers in new environments.

### Deploying a container

Usage: quick-lxc-deploy &lt;debian version&gt; &lt;architecture&gt; [&lt;mirror&gt;]

quick-lxc-deploy takes care of:

* fetching predefined set of packages and packing them into tarball in your ${HOME}/Downloads directory
* installing new container in ${HOME}/lxc directory
* creating SSH key files in ${HOME}/.ssh/lxc_rsa for root and current user (for speed-dialing with lxcssh)
* creating an account for current user on a target container with bind-mounting home directory from /home/${USER}-${container}


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

