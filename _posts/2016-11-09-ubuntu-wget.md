---
layout: post
title: ubuntu wget 乱码解决、批量下载
tags: [wget、乱码、批量下载]
---

## 下载服务器电影时候遇到乱码，下载下来的文件名都是乱码 或者是 无效的编码。

> Linux 中没有文件“后缀名“的概念。Linux认为文件名是一个整体。

* 解决方法：
正解是参数 `--restrict-file-names=nocontrol`    
完整命令`wget --restrict-file-names=nocontrol 资源地址`  

## wget命令的批量下载功能   

* 例如，自动下载http://www.lsqboy.com/movie/下面的所有文件：  

代码示例：  
`wget -nd -r -l1 --no-parent http://www.lsqboy.com/movie/`

>  注：
   -nd 不创建目录；-r 递归下载；  
   -l1只下载当前目录下的文件；  
   –no-parent 不下载父目录中的文件。  

* 指定下载制定后缀的文件，例如只下载http://www.lsqboy.com/movie/下`.mp4`文件和`.mkv`文件：  
 
代码示例:    
`wget -nd -r -l1 --no-parent -A.mp4 -A.mkv http://www.lsqboy.com/movie/`  


* 下载网站目录下的除html 之外的文件和目录，且不遵守robots.txt的限制。  

可以这样：  
`wget -c -r -np -k -L --reject=html http://www.lsqboy.com/moive/ -e robots=off`
 