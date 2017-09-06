---
layout: post
title: adb,fastboot常用命令及刷机技巧
tags: [android, adb, sideload, fastboot,摘录]
---

此篇讲的内容是Android Debug Bridge（简称adb）的使用方法，学会它可以让你的刷机工作事半功倍！  

## I. 安装驱动

使用adb的前提条件是安装相应机型的驱动，以便使计算机识别你的机器。

## II. 使用ADB

在此下载最新版的ADB [https://pan.baidu.com/s/1gdeivdx](http://pan.baidu.com/s/1gdeivdx) 下载后解压，你会看到一个adb.exe 文件，
在当前文件夹按住shift再点右键，在弹出的菜单里选择在此打开命令窗口（win7下），win7以下系统可以将文件解压至C:/windows下，即可直接使用adb命令   

### 写在前面  

当你启动一个adb客户端，adb会先检测是否已经存在一个adb的服务器，如果没有，新的客户端会绑定本机的5037端口（TCP） 而客户端（即手机）会启动两个  

### 测试  

在cmd中输入 adb version 在此应该返回如下文字（意思是查看adb版本）  

    Android Debug Bridge version 1.0.31  

### 调试模式  

如果你希望使用adb管理手机，那就必须开启手机的开发者选项里的调试模式，并且信任正在使用的计算机 如果设置OK，输入以下命令  

    adb devices  
    
就可以看到你的手机啦！这个命令就是查看系统连接设备的命令，这里可以有多个设备  

    List of devices attached  
    0527dac2002e9b36        device  
    #注意（0527dac2002e9b36是手机的临时ID，每次可能都不一样，为的是方便计算机管理） 
 
### 网络调试  

细心的读者可能眼睛比较亮，已经发现了开发者选项里多了一个网络ADB调试选项，他可以让你远程调试处于同一局域网里的android手机啦！ 打开此选项后会出现一个
IP地址和端口号（老高的地址为192.168.1.101:5555），在cmd中输入  

    adb connect 192.168.1.101:5555 再输入 adb devices 显示  
    List of devices attached  
    192.168.1.101:5555      device  
    
意思就是远程已经连接到你的手机设备，以后的调试都可以在无线模式下进行，是不是很方便呢？ （注意：如果使用此命令的时候没有效果，请注意你是不是已经把数据线拔了）  

## III. 常用命令

```
    adb devices                         #显示设备信息
    adb install 123.apk                 #安装一个软件
    adb uninstall -k 123.apk            #删除一个软件
    adb shell                           #进入shell环境
    adb push c:/1.txt /sdcard/sdir/     #向设备推送文件
    adb pull /sdcard/1.txt C:/          #从设备取回文件
    adb reboot bootloader/recovery      #使手机重启进入BL或RE
```

## IV. 刷入RECOVERY

一般官方的ROM的RE在第三方ROM上做了很多限制，如果要刷第三方ROM，替换RE是第一步 方法很简单，先下载对应机型的RECOVERY包 五太子常用的是CWM、TWRP，
一个非触屏，一个触屏版。推荐使用CWM6.0以后的版本，因为会有新加入的sideload功能，可以让你不用事先将ROM包拷贝至SD卡或手机内存。  

### 解锁手机  

下载好ROM包后先不要急，刷RE的前提是手机必须解锁，如果你的手机在开机出现谷歌字的时候下面有一个小锁，并且锁是被打开的，那么恭喜你，你的手机已经解锁，
如果没有解锁，可以下载CF-Auto-Root，连ROOT，带解锁，已经解锁的请进入下一节。  

> 注意，解锁会清空所有数据，所以一定注意要保存数据。  

首先你需要将设备进入BL模式，该模式也可以称为引导模式，进入方法为关机状态下按开机+音量加。如果看到屏幕开机并没有进系统，那就意味着你已经进入了BL模式，
运行root-windows.bat，稍等片刻就root并解锁好了。  

### 再次进入BL    

关机状态下按开机+音量加，进入BL模式，手机连上电脑，输入`adb devices`查看是否连接成功！  

> 请再次注意，如果你的手机没有解锁，那么这一步一定不会成功，除非你解完锁又上锁了  

### 刷入RE  

如果上一步成功，那么你离成功只有一步之遥啦 使用这个命令  

    fastboot flash recovery recovery.img  
    
recovery.img指的是RE包的名字，若出现类似"sending 'recovery' (10000KB)"的提示，那么你的RE刷入成功！  

## V. 使用RECOVERY刷ZIP包
此方法俗称卡刷，与此对应的还有线刷。 线刷更彻底，卡刷更方便。现如今，RE中加入了sideload功能，使卡刷变得比线刷还方便。 RE刷ROM再此就不多说了，此篇
主要想讲讲sideload  

### 使用sideload  
sideload大大简化了刷机的步骤，以往的方法刷机前需要将ROM包拷贝至SD卡或者手机内存，才能进行刷机。而sideload功能可以直接将刷机包导入手机并开始刷机，
期间只需要一条命令即可！  

使用sideload前必须开启sideload，开启方法如下    
 * CWM在刷ZIP包选项的下面有个从sideload刷机  
 * TWRP在高级选项里开启
      
当开启了sideload模式后，就可以使用下面的命令进行刷机   

    adb sideload 刷机包名称.zip   

## VI. fastboot命令
### 说明
当手机进去fastboot模式的时候，PC端就可以使用fastboot命令操作更低层的东西啦！
  
### 常用命令
#### 擦除分区

    fastboot erase {partition}     
    例：  
    fastboot erase boot  
    fastboot erase system  

#### 烧写指定分区

    fastboot flash {partition} {*.img}  
    例：  
    fastboot flash boot boot.img  
    fastboot flash system system.img  

#### 烧写所有分区

    fastboot flashall  
    注意：此命令会在当前目录中查找所有img文件，将这些img文件烧写到所有对应的分区中，并重新启动手机。  
    
#### 一次烧写boot，system，recovery分区  
 1. 创建包含boot.img，system.img，recovery.img文件的zip包。
 2. 执行：`fastboot update {*.zip} ` 

#### 烧写开机画面

    fastboot flash splash1 开机画面.bmp  

#### 重启手机

    fastboot reboot  

#### 重启到bootloader 刷机用

    fastboot reboot-bootloader  

#### Nexus5的TWRP下载地址及刷机命令  

1. 先把下载下来的img文件重命名为re.img    
2. 使用命令 `fastboot flash recovery re.img`  
3. 刷入nexus5刷入recovery成功   

