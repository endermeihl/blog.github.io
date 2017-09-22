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
# iftop -F 10.10.1.0/24或# iftop -F 10.10.1.0/255.255.255.0
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
<font color="black" size="4" style="font-weight:bold;font-style:italic;" face="黑体">以上的参数界面启动以后可以直接作为界面内命令使用</font>
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


### 软连接和硬连接