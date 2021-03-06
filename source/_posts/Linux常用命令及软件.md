---
title: Linux常用命令及软件
date: 2017-03-02 10:36:31
tags: 
  - Linux
categories:
  - 技术文档
  - Linux
---

### 流量监控软件：iftop
iftop 需要基本依赖 libpcap 和 tcpdump
#### 界面说明
中间的<= =>这两个左右箭头，表示的是流量的方向
同时大小用黑色长条标尺按比例标识
**TX**：发送流量
**RX**：接收流量
**TOTAL**：总流量
**Cumm**：运行iftop到目前时间的总流量
**peak**：流量峰值
**rates**：分别表示过去2s、10s、40s的平均流量
#### 常用参数
**-i**  设定监测的网卡，如：
```bash
# iftop -i eth1
```
**-B** 以bytes为单位显示流量(默认是bits)，如：
```bash
# iftop -B
```
**-n** 使host信息默认直接都显示IP，如：
```bash
# iftop -n
```
**-N** 显示端口号，如: 
```bash
# iftop -N
```
**-F** 显示特定网段的进出流量，如:
```bash
# iftop -F 10.10.1.0/24 或 
# iftop -F 10.10.1.0/255.255.255.0
```
**-h** 帮助，显示参数信息
**-p** 使用这个参数后，中间的列表显示的本地主机信息，出现了本机以外的IP信息;
**-b** 使流量图形条默认就显示;
**-f** 过滤计算包用的;
**-P** 使host信息及端口信息默认就都显示;
**-m** 设置界面最上边的刻度的最大值，刻度分五个大段显示，如：
```bash
# iftop -m 100M
```
<font color="red" size="4" style="font-weight:bold;font-style:italic;" face="黑体">以上的参数界面启动以后可以直接作为界面内命令使用</font>
<!-- more -->

### 定时任务设置
#### 使用crontab的基本命令
**-e** 编辑crontab服务文件
**-l** 查看用户的定时任务
**-r** 删除某个任务
**-u** 指定用户
#### crontab的文件语法
<table><tr><th>分</th><th>小时</th><th>日</th><th>月</th><th>星期</th><th>命令</th></tr><tr><th>0-59</th><th>0-23</th><th>1-31</th><th>1-12</th><th>0-6</th><th>Command</th></tr></table>
**“*”**代表取值范围内的数字
**“/”**代表“每”
**“-”**代表从某个数字到某个数字
**“,”**分开几个离散的数字
可以直接修改/etc/crontab文件
举例如下：

### Linux权限管理
- 文件权限符
首先是类型：
**"-"** 代表文件
**"d"** 代表目录
**"c"** 代表字符型设备
**"b"** 代表块设备
**"n"** 代表网络设备

- 3组三字符构成的权限标识码
**"r"**代表对象是可读的
**"w"**代表对象是可写的
**"x"**代表对象是可执行的

- 3组字符各表示
对象的属主
对象的属组
系统的其他用户

- 默认用户权限
由umask来确定，注意umask表示的其实是屏蔽掉的权限

- 权限变更
使用chmod来变更权限
使用方式
```bash
# chmod options mode file
```
还可以使用符号模式
**"u"**代表用户
**"g"**代表组
**"o"**代表其他
**"a"**代表以上所有
**"+"**代表增加权限
**"-"**代表移除权限
同时可以使用**"-R"**让权限改变递归到作用的文件和子目录

- 改变所属关系
使用chown改变文件所属
使用chgrp命令改变文件的属组
使用方式
```bash
# chown option owner[.group] file
```
<font color="red" size="4" style="font-weight:bold;font-style:italic;" face="黑体">只有root用户可以改变文件的属主。任何属主都可以改变文件的属组，前提是属主必须是源和目标属组的成员</font>

chgrp使用方式
```bash
# chgrp group newfile
```

- 共享文件
通过设置组ID完成新建文件对属组的共享 


### 链接文件
- 符号链接，软链接
```bash
# cp -s file link
```
**"-s"**参数创建一个符号链接，称为软链接
- 硬链接
```bash
# cp -l filey filenew
```
硬链接创建了一个独立文件，引用硬链接文件等同于引用了源文件


### 用户和组管理