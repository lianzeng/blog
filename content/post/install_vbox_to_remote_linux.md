---
title: "Install virtualbox remotely in linux"
date: 2019-09-05T15:25:07+08:00
draft: false
---

<br />
   
    
steps:  
0. enable vtx in bios for linux host;   
1.install virtualbox on linux host:  
https://tecadmin.net/install-virtualbox-on-ubuntu-18-04/     

2.install Vagrant on linux host, 使用这个工具可以自动化的在virtualbox里面安装操作系统, 不要使用 apt install 安装vagrant ，应该直接去官网下载二进制包安装;    
https://www.vagrantup.com/intro/getting-started/install.html  , Note:  if host is ubuntu, download Debian package,       

3.intall centos inside virtualbox by vagrant tool:     
copy a sample Vagrantfile to linux host, then excute "vagrant up" on the same dir , you can edit Vagrantfile to set the cpu/disksize/memory/ip/hostname,disksize default is 40GB, if want modify disksize,need install plugin first (vagrant plugin install vagrant-disksize) ;
在线安装centos 比较慢，容易失败，建议先下载好centos镜像到本地，然后再添加本地镜像: vagrant box add centos7  local/path/to/centos7.box
再修改Vagrantfile:   config.vm.box = "centos7" , 再运行: vagrant up , 成功后，在Vagrantfile 所在目录下会有 .vagrant/ 目录，   top 命令就可以看到 VBoxHeadless 进程了；
安装完成后，host会有vboxnet0 interface, 可以和各个vbox 通信;     

4.查看所有虚拟机状态 :  vagrant global-status, 必须得进入到Vagrantfile 所在目录执行这个命令才行;    

5.enter vm:  vagrant ssh <name>    
  exit vm :  logout   

6.initial root pwd:   
sudo su ;  passwd ;   


7.modify ssd_config in each vm, so can root ssh  to vm :  
sudo su     
vi /etc/ssh/sshd_config:   
PasswordAuthentication yes   
then : service sshd restart     
