---
layout: post
title: Ubuntu 使用体验
tags: [ubuntu]
---

> 基于ubuntu 16.04 使用体验， 希望对大家有所帮助


### 系统网络代理

1. 可以注册个谢公屐，购买翻墙服务，一年200RMB
2. ubuntu系统设置 --> 网络 --> 网络代理 --> 配置URL（C）
3. 填入谢公屐的`PAC路径地址` 应用到整个系统.
4. 完成 ..


### Chrome安装

1. 添加Key :  
   `wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add - `
2. 添加源 :  
    `sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'`
3. 更新源、安装chrome :   
   `sudo apt-get update`  
   `sudo apt-get install google-chrome-stable`
4. 完成..


### 字体库的安装

1. [MSYH字体下载](http://zh.osdn.jp/projects/sfnet_allfonts/downloads/msyh.ttf/)  
   或者 可以在 win10系统盘 --> Windows --> Fonts  下面拿 .ttf格式的字体
2. sudo apt-get install font-manager
3. ![fonts](/images/posts/2016-08-02/fonts.png)
4. 完成 ..


### JDK的安装
1. 添加、更新源：
    - sudo add-apt-repository ppa:webupd8team/java
    - sudo apt-get update
2. sudo apt install oracle-java8-installer
3. 终端运行 `java -version` 有看到版本信息则为安装成功。


### Android Studio的安装

1. [Android Studio 下载](https://developer.android.com/studio/index.html#linux-bundle)
2. 解压...解压路径最好不要有中文。终端下解压命令：`tar xfz ***.tar.gz`
3. 运行...运行前需要机子已经安装好JDK.  
   用终端进入解压目录下的`bin`子目录 下，然后在终端下运行启动命令：`./studio.sh`
3. 完成 .. 


### 安装主题管理工具

1. 添加源: sudo add-apt-repository ppa:freyja-dev/unity-tweak-tool-daily
2. 更新源: sudo apt-get update
3. 安装： sudo apt-get install unity-tweak-tool
4. 完成.. 主题 --> 图标 --> Numix-circle 


### 安装国际版QQ

1. [下载QQ安装包](http://yun.baidu.com/share/link?shareid=2983202140&uk=202032639)
2. 解压。得到wine-qqintl文件，里面有  
    `fonts-wqy-microhei_0.2.0-beta-2_all.deb`  
    `ttf-wqy-microhei_0.2.0-beta-2_all.deb`   
    `wine-qqintl_0.1.3-2_i386.deb`
3.  依次安装：  
    sudo dpkg -i wine-qqintl_0.1.3-2_i386.deb  
    sudo dpkg -i ttf-wqy-microhei_0.2.0-beta-2_all.deb  
    sudo dpkg -i fonts-wqy-microhei_0.2.0-beta-2_all.deb 
        
    > 在安装中发生了错误，原因是还有lib没有配置，所以再输入sudo apt-get install -f


### 安装WPS

1. [下载WPS](http://www.ubuntukylin.com/application/show.php?lang=cn&id=278)
2. sudo dpkg -i wps-office_10.1.0.5630-a20p1_amd64.deb  
3. 完成..

   > 在安装中发生了错误，原因是还有lib没有配置，所以再输入sudo apt-get install -f


### 安装搜狗输入法

1. [下载搜狗输入法](http://pinyin.sogou.com/linux/download.php?f=linux&bit=64)
2. sudo dpkg -i sogoupinyin_2.0.0.0078_amd64.deb  
3. 重启电脑，此步很关键
4. 打开`Fcitx设置`，添加搜狗输入法，完成..

   > 在安装中发生了错误，原因是还有lib没有配置，所以再输入sudo apt-get install -f

      






