---
title: linux
date: 2021-04-21 10:38:32
tags:
---

## 前言
### why
1. 为什么要学linux
- 开源、免费的操作系统
- 安全性、稳定性、处理多并发得到业界的认可
- 很多中型、大型甚至巨型项目都在使用linux

2. ibm aix,sun solaris,hp unix,bsd 伯克利分校,minux 都是基于unix开发的系统
- linux是linus这个人把基于unix开发minux嵌入到个人电脑中优化的一个系统
- redhat、fedora、SUSE、红旗Linux 都是基于linux的二次开发，比如加一个界面
  - 因为他们的内核都是linux

3. 工作原因 
- 基于windows的程序员开发已经饱和了
- 开源、免费

4. 角色分类
- linux系统管理员 - 系统的管理
- linux程序员 - 编程，可以在linux上开发用编程语言C++/Java之类的
  - linux 软件工程师（pc）
  - linux 嵌入式开发（单片机、芯片）

### how 学习方法 - 噗，目标只学会第一点
- linux平台上的开发、包括vi,gcc,gdb,make,jkd,tomcat,mysqk..和linux基本操作
- 加厚编程功底
- 学习unix高级环境编程
- linux开发方向选择
- 思考 - 实践 - 再思考 - 再实践

### linux内容
1. 基础部分
- linux基础知识
- linux 常用命令80个（总共有4000多个命令）
- linux分区、vi、权限

2. 实用部分
- Samba安装与配置
- linux网络环境配置
- crontab使用
- jdk/apache/mysql/ssh/rpm安装与配置
- linux下java网络编程
- shell初步介绍
- 《鸟哥的linux》
- 《linux从入门到精通》
- 《linux内核完全剖析》

## 入门
### linux的特点
1. 开源
2. 支持多线程、多用户
3. 安全性好
4. 对内存和文件管理优越
- linux最小只需要4M就可以跑起来，window最少需要64M
  - 可以做嵌入式开发，直接把linux嵌入手机
- linux 2004年500强已经有280席
- linux 操作困难
- 1994 - 至今

### 安装VMware虚拟机，在虚拟机安装linux操作系统
- VMware Workstation 16.1.1 Player 普通应用程序安装
- 虚拟机上安装了CentOS 8 64位的linux 硬盘空间我给了40G
- 还需要下载ISO映像文件  
  - http://mirrors.huaweicloud.com/centos/8.3.2011/isos/x86_64/
  - ISO：就是带桌面的linux系统，比较大
  - menifest：就是不带桌面的linux系统，自然比较小
  - torrent：是种子文件，相当于下载其他软件的MD5,用来校验你下的对不对
  - 我用的DVD
  - 虚拟机上只能识别到ISO格式的，所以只下这种就完事儿了
- 启动虚拟机
- 开始一大堆配置
  - https://www.tqwba.com/x_d/jishu/334612.html
- 进入linux系统，是图形化界面，想违背了我学习的初衷，转变为命令行界面：
  - 图形 -> 命令行：Ctrl+Alt+F3 OR `systemctl set-default multi-user.target` OR `startx`
  - 命令行 -> 图形：Ctrl+Alt+F1 OR `systemctl set-default graphical.target`
  - 图形化界面真的卡的不要不要的 还是别玩图形化了

### linux命令
- 
- 关机命令






> 声明：本站所有内容仅供个人学习娱乐笔记所用，如涉侵权，请联系删除