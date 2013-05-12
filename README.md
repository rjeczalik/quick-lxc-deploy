quick-lxc-deploy
================

Couple of bash scripts hacked together for effortless deploying/accessing debian-based containers.

### Why?

Educational purposes. For fully featured lxc manager you may want to try:

* https://github.com/fgrehm/vagrant-lxc
* https://github.com/lxctl/lxctl
* http://libvirt.org/drvlxc.html

### Usage

```
Usage: qlxc help   (prints this help message)
       qlxc deploy <distro name> amd64|i386 [<container name>]
       qlxc ssh    [<hostname or index>]    [<command>]
       qlxc start  [<hostname or index>]
       qlxc stop   [<hostname or index>]
       qlxc rm     [<hostname or index>]
```

### Example usages:

To deploy Ubuntu Raring (x86_64) with default hostname (raring-amd64):

`qlxc deploy raring amd64`

To echo hostname of first container:

`qlxc ssh 0 "echo \$(hostname)"`

### Features

qlxc takes care of:

* fetching predefined set of packages and packing them into tarball in your CACHE_DIR directory
* installing new container in DEPLOY_DIR directory
* creating SSH key files in ~/.ssh/lxc_rsa for root and current user (for speed-dialing with qlxc ssh)
* creating an account for current user on a target container with rbind-mounting user's home directory
* starting/stoping/removing containers

### Configuration file - ~/.qlxc.conf

qlxc uses the following options:

* PACKAGES - additional packages list to be included into container
* CACHE_DIR - path to directory storing debootstrap's tarballs
* DEPLOY_DIR - prefix path for container rootfs

qlxc ssh
======

Speed-dial-like access to a container.

### Speed dialing

Typical qlxc ssh output:

```
[rjeczalik@rjeczalik-ub64 rjeczalik]$ qlxc ssh

  [0] lenny-amd64 (10.0.3.132)
  [1] lenny-i386 (10.0.3.166)
  [2] squeeze-amd64 (10.0.3.107)
  [3] squeeze-i386 (10.0.3.190)

```

qlxc ssh connects to a container as current user - e.g. in order to login as root to squeeze-amd64 container call

`sudo qlxc ssh 2`
