---
title: "Hello, Hugo"
date: 2019-08-29T15:25:07+08:00
draft: false
---

<br />
   
    

建立https博客步骤：   
1）先在aliyun购买一个云主机（带公网ip，最好是香港的）;   
2）在阿里云万网购买域名，并在上面操作，绑定域名到云主机ip,这步需要实名认证；   
3）在云主机安装nginx 并配置，监听端口80;   
4) 在github建一个repo, 用来存储blog资源;   
5）clone hugo到本地，写文章，并推送到刚刚建立的repo;   
6) 把repo添加到travis-ci.org,  在repo上配置.travis.yml文件，这样每次有新文章提交到repo都会触发travis ci build，然后会自动把编译结果同步到云主机的nginx location目录，这样网站就会同步更新,注意不要把repo添加到travis-ci.com,因为.com是收费的,查看build history: https://travis-ci.org/lianzeng/blog/builds ；   
7) 把本地电脑的~/.ssh/id_rsa.pub 放到云主机的~/.ssh/authorized_keys, 然后把本地的id_rsa 用travis encrypt-file工具加密为id_rsa.enc, 再上传到repo,这样travis ci build完后就有权限把结果同步到云主机中，参考https://docs.travis-ci.com/user/encrypting-files/ ；         
8）把nginx http website转为https，很简单，而且证书通过定时脚本自动更新，永不过期，参考https://coolshell.cn/articles/18094.html ;



