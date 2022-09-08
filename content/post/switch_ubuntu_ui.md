---
title: "Switch Ubuntu desktop environment between GUI only envrionment"
date: 2022-09-02T21:51:57+08:00
draft: false
tags : ["Ubuntu"]
---

This is how we turn on/off the Ubuntu desktop environment

## Disable UI desktop on Ubuntu
```
$ sudo systemctl set-default multi-user
$ sudo reboot
```

## Enable UI desktop on Ubuntu
```
$ sudo systemctl set-default graphical
$ sudo reboot
```