---
layout: post
title: Ubuntu 分区方案
tags: [linux]
---

> ubuntu 分区方案，个人总结。


### 高级用户Desktop安装建议： 
 
挂载点 | 装置 |说明  
/（主分区、ETX4）  |  /dev/hda1 | 10~15G足以  
/boot（逻辑分区、ETX4）  |  /dev/hda2 | 100M即可  
/home（逻辑分区、ETX4）  |  /dev/hda3 | 最大剩余空间  
Swap（逻辑分区）  |  /dev/hda5 | 大约内存大小（至少512MB）  


### 高级用户Server安装建议：  

挂载点 | 装置 |说明  
/（主分区、ETX4）  |  /dev/hda1 | 10~15G足以  
/boot（逻辑分区、ETX4）  |  /dev/hda2 | 100M即可  
/home（逻辑分区、ETX4）  |  /dev/hda3 | 最大剩余空间  
/var（逻辑分区、ETX4）  |  /dev/hda6 | 视服务器功能决定大小，至少需要1GB以上  
Swap（逻辑分区）  |  /dev/hda5 | 大约内存大小（至少512MB）  


