---
title: 使用python调用http请求实现备份
date: 2017-08-22 16:23:00
tags:
 - python
categories:
 - python
---
表面上使用python调用http请求，实际是使用队列实现定时备份的一部分
    整个业务逻辑为：
   - 1.启用linux定时任务
        crontab -e
        定时调用python脚本
   - 2.python执行http请求
   - 3.http请求对应的是API接口
        接口负责根据请求想任务队列里提交队列
   - 4.ActiveMQ管理的队列
   - 5.队列监听服务监听队列并处理任务

附上python的代码,代码使用了文件读写，时间处理和http请求，属于比较有用的python作为脚本的案例
```python
#!/usr/bin/python3
# -*- coding: utf-8 -*-

import http.client
import datetime
import os

BASE_DIR = os.path.dirname(__file__)


def get_projectfile(filename):
    return os.path.join(BASE_DIR, filename)


def _set_date(new_date):
    with open('date.res', mode='w+', encoding='utf-8') as f:
        f.write(new_date)
        f.flush()


def _get_date():
    datetemp = []
    with open(get_projectfile('date.res'), 'r', encoding='utf-8') as f:
        for line in f.readlines():
            datetemp.append(line.strip())
    return datetemp


def _add_date(date):
    dt = datetime.datetime.strptime(date, "%Y%m%d")
    d = dt + datetime.timedelta(hours=24)
    new_date = d.strftime('%Y%m%d')
    return new_date


def backupold():
    try:
        url = []
        date = _get_date()[0]
        print(date)
        url.append("api.junruizx.com")
        url.append(80)
        data = "targets=exam,train,vrexam&startday=" + date + "&days=1"
        url.append("schedule/backup?" + data)
        client = http.client.HTTPConnection(url[0], url[1], timeout=30)
        client.request('GET', "/" + url[2])
        response = client.getresponse()
        _set_date(_add_date(date))
        print(response.status)
    except Exception as e:
        print('except:', repr(e))
    finally:
        if client:
            client.close()


backupold()
```