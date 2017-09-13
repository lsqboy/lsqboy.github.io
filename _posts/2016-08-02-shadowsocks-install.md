---
layout: post
title: Ubuntu 搭建 ShadowSocks
tags: [linux]
---

> 分享下之前同事教我搭建SS的过程，步骤。  
  希望对大家有所帮助。


1. add the GPG public key to your system:  
   $ wget -O- http://shadowsocks.org/debian/1D27208A.gpg | sudo apt-key add -

2. 添加源  
   - vim /etc/apt/sources.list.d/ss.list
   - deb http://shadowsocks.org/debian wheezy main
   - touch ss.list  
   或  
   - echo "deb http://shadowsocks.org/debian wheezy main">> /etc/apt/sources.list.d/ss.list  

3. 更新源 
    - sudo apt-get update    
    - sudo apt-get install shadowsocks 

    > 
        安装时候遇到的问题:(google搜索 init-system-helpers ubuntu 14.04)  
        cd /tmp/      //缓存文件夹  
        wget http://launchpadlibrarian.net/173841617/init-system-helpers_1.18_all.deb  //下载文件  
        sudo dpkg -i init-system-helpers_1.18_all.deb //安装文件
4. 编辑配置文件：  
   - sudo vim /etc/shadowsocks-libev/config.json  
   
   >
        {  
            "server":"lsqboy.com",  
            "server_port":8080,    
            "local_port":1888,    
            "password":"lsqboy",   
            "timeout":60,  
            "method":"aes-256-cfb"    
        }  
    
5. 编辑默认设置  
   - sudo vim /etc/default/shadowsocks-libev   
   DAEMON-ARGS=”-A --fast-open”   //修改成 实验性(-A)  快速打开tcp(--fast-open)

6. 编辑服务是server还是local   
   sudo vim /etc/init.d/shadowsocks-libev  
   DAEMON=/usr/bin/ss-local  //客服端模式  
   DAEMON=/usr/bin/ss-server  //服务端模式

7. sudo update-rc.d shadowsocks-libev defaults //添加一个服务   
   sudo update-rc.d shadowsocks-libev enable //服务启用
   - 添加一个服务: sudo update-rc.d 服务名 defaults 99  
   - 删除一个服务: sudo update-rc.d 服务名 remove
   
8. sudo service shadowsocks-libev status //查看服务状态  
   sudo service shadowsocks-libev restart/start/stop //启动\停止服务

9. sudo lsof -i:1888 //查看端口使用情况  
   ss-local 10351   root    3u  IPv4 720047      0t0  TCP localhost:1888 (LISTEN)  
   ss-local 10351   root    4u  IPv4 720049      0t0  UDP localhost:1888 

10. 设置中Network 里面的Proxy修改成  [http://lsqboy.com/public/ss.pac](http://lsqboy.com/public/ss.pac)

保存.大功告成..

参考链接：[安装shadowsocks](https://shadowsocks.org/en/download/servers.html)



