---
layout: post
title: Openstack, Openshift, CloudFoundry
author: Ethan
---

## 1. Openstack

#### 笔记本上安装devstack

    adduser stack

    apt-get install sudo -y || yum install -y sudo
    echo "stack ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

    sudo apt-get install git -y || yum install -y git
    git clone https://github.com/openstack-dev/devstack.git
    cd devstack && ./stack.sh

    安装过程中会提示输入MySQL, RabbitMQ, OpenStack Dashboard 和 Keystone 的密码，默认密码是随机的；
    最后报错 'Access denied for user 'root'@'localhost'；
    这里devstack是用mysql的root密码连接的，访问keystone报错。
    之前安装了gitlab设置了mysql的root密码，这里在提示MySQL administrative password时改成了输入这个密码就可以了。

    最后可以访问dashboard (aka Horizon)了，输入用户名admin或demo和之前输入的密码（可以在stackrc/localrc修改）登录 。




