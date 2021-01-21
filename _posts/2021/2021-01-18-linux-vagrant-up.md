---
title: Setup a Linux VM on Virtual Box with Vagrant
date: 2021-01-20
category: linux
tags: 
  - linux
  - sysadmin
---

# Introduction

A common method of installing Linux is with an installation DVD, or DVD ISO file for virtual enviorments. However, vagrant is a powerful tool for managing virtual machines which you can use to boot and manage a Linux VM on your local computer.

## Goals

- Setup a Linux VM on Oracle Vitual Box using Vagrant
- SSH access into the Linux VM to administer the VM

## Table of Contents

- [Introduction](#introduction)
  - [Goals](#goals)
  - [Table of Contents](#table-of-contents)
  - [Prerequisites](#prerequisites)
- [Setup the VM with Vagrant](#setup-the-vm-with-vagrant)
- [SSH](#ssh)
- [Vagrant usage and commands](#vagrant-usage-and-commands)

## Prerequisites

- [Oracle Virtual Box](https://www.virtualbox.org/)
- [Vagrant](https://www.vagrantup.com/)

# Setup the VM with Vagrant

Create a project directory for a vagrant configuration file (vagrantfile). Vagrant has a [catalog](https://app.vagrantup.com/) of base images available (e.i: `centos/8`). `vagrant init centos/8` to create a base CentOS 8 vagrantfile and `vagrant up` to start and provision the enviorment.

```
$ mkdir vagrant
$ cd vagrant
$ vagrant init centos/8
$ vagrant up
```

# SSH

`vagrant ssh` to start an SSH session into the enviorment. `exit` to exit the SSH session.

```
$ vagrant ssh
Last login: Thu Jan 21 05:05:05 2021 from 10.0.2.2
Last login: Thu Jan 21 05:05:05 2021 from 10.0.2.2
[vagrant@localhost ~]$
```

This approach allows access to the shell, but more SSH configuration information might be needed to access the shell through a regular SSH client like so:

```
$ vagrant ssh-config
Host default
  HostName 127.0.0.1
  User vagrant
  Port 2222
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  PasswordAuthentication no
  IdentityFile C:/Users/steva/centos-7-vagrant/.vagrant/machines/default/virtualbox/private_key
  IdentitiesOnly yes
  LogLevel FATAL
```

Confirm these settings can start an SSH session:

```
$ ssh vagrant@127.0.0.1 -p 2222 -i C:/Users/steva/centos-7-vagrant/.vagrant/machines/default/virtualbox/private_key
```

# Vagrant usage and commands

`vagrant --help` displays usage and commands. Most people might need a hanful of these commands to simply `suspend`, `resume`, and `destroy` the VM.