# WIP

# Try it yourself ...

* it's easy to start and stop services on clients.
* install operating system updates on multiple machines
* Reboot client after kernel updates

![concept yadtshell and yadtminion](https://raw.github.com/yadt/try-it-yourself/master/images/yadtshell_to_yadtclient.png)

In this guide we want to show you how to set up a minimal YADT system, on two hosts with real world services to play with.
the ```yadtshell``` on the first server is the controlling instrument, the ```yadt-minion``` is the client component.

## Prerequisites
* a RHEL based system version 6.x (preferred).
* python >= 2.6.
* a user with sufficient rights to install/remove packages via `sudo yum`.
* All hosts to be controlled are accessible **passwordless** via ssh.
* EPEL has to be installed. You will find the rpm on [The newest version of 'epel-release' for EL6](http://download.fedoraproject.org/pub/epel/6/i386/repoview/epel-release.html), for example


## install the rpms
create [or Download](https://raw.githubusercontent.com/yadt/try-it-yourself/new_howto/yadt.repo) this file on your testmachines; this adds our repository to your RHEL based system.
```
/etc/yum.repos.d/yadt.repo
```
```bash
[yadt]
name=yadt repo
baseurl=http://dl.bintray.com/yadt/rpm
gpgcheck=0
```
check the repository with
```bash
sudo yum repolist
```

you will see something like this:
```bash
...
extras                      CentOS-6 - Extras       14
updates                     CentOS-6 - Updates      1.104
yadt                        yadt repo               4
repolist: 18.467
```
## Installation

Now you can use ```yum``` to install the yadt components on your servers

on the "master" server:

```[vagrant@yadtshell-testmachine ~]$ sudo yum install yadtshell```

on the client server:

```[vagrant@minion-testmachine ~]$ sudo yum install yadt-minion```


## configuration of the yadt-minion

### tl;dr

save this snipplet as ```/etc/yadt.conf.d/10_postfix.yaml```(4 **blanks** no **tabs**)

```yaml
services:
    postfix:
```

### long version

The yadt-minion gets conﬁgured via ```*.yaml``` ﬁles in the
```/etc/yadt.conf.d/``` directory; they get merged in alphanumeric
order. Please note Indented blocks have to start with **4 blanks**.

the yadt-minion rpm provides its default configuration as ```00_defaults.yaml```.
please check the [wiki](https://github.com/yadt/yadtshell/wiki/Host-Configuration) or [cheatsheet](http://www.yadt-project.org/cheatsheet/cheatsheet.pdf) for further information about service configuration.


## configuration of the yadtshell

you can run ```yadtshell``` commands on _targets_, a _target_ is a set of hosts which belong together. check the [wiki](https://github.com/yadt/yadtshell/wiki/Target)
or the [cheatsheet](http://www.yadt-project.org/cheatsheet/cheatsheet.pdf) for further information.

```target```

```yaml
hosts:
- minion-testmachine
```

## using the yadtshell


