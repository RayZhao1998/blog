---
title: 服务器部署 Flask 项目指北
tags: 
	- 开发
	- 后端
	- Flask
---
## 用到的工具
- Flask + Flask-RESTful
- virtualenv
- mysql
- docker(尚未使用)

## Flask-RESTful
之所以用 RESTful 是因为不想用 Flask 提供的前端模板，同时希望能够给客户端提供接口，所以想到使用 Flask-RESTful。

[Flask-RESTful 文档](https://flask-restful.readthedocs.io/en/latest/) 提供了非常完整的例程和文档解释。
## Flask + gunicorn 部署
之前看关于 Flask 服务器部署的相关文章说，单纯用`app.run(debug=True)`这样的方式会很不稳定，[Flask —— 独立 WSGI 容器](http://docs.jinkan.org/docs/flask/deploying/wsgi-standalone.html)中提到了如何在服务器上部署，这里我用到的是`Gunicorn`

<!-- more -->
需要注意的一点是，这里绑定的`ip`不能是`127.0.0.1`而应该是`0.0.0.0`，包括后面的`mysql`也是，具体原因还没用弄清楚，大概是因为`127.0.0.1`是允许了`localhost`访问，外网是无法访问的

```shell
gunicorn -w 4 -b 0.0.0.0:4000 myproject:app
```

`-w 4`是指用四个 worker 进程，`myproject:app`中`myproject`为文件名（去除`.py`），`app`是指文件中实例化 Flask 的变量名

### 关于开放端口与安全组设置
阿里云的服务器上有特殊的安全组设置，出方向是全端口，但是入方向需要自己去设置，**端口范围**即你需要用到的端口，**授权对象**可填`0.0.0.0/0`。

关于开放端口，通过`iptables -L`查看端口开放状态![iptables](https://s1.ax1x.com/2018/09/09/iiEuJx.png)

开放端口的方法也很简单，可以使用`iptables`开放端口
```
iptables -A INPUT -p tcp --dport 8000 -j ACCEPT
iptables -A OUTPUT -p tcp --sport 8000 -j ACCEPT
```

## Flask 的 mysql 操作
Flask 的 mysql 操作需要用到`SQLAlchemy, pymysql, MySQLdb`。

看到很多关于 python mysql 的文章中都说引入 mysql-python,亲测后发现报错
```
No module named 'ConfigParser'
```
google 后发现是因为 python3.* 中无 ConfigParser, 解决方案为直接`pip install PyMySQL`
使用方法
```python
import pymysql
pymysql.install_as_MySQLdb()
import MySQLdb
```

然后再根据`flask_sqlalchemy的SQLAlchemy`文档查看 flask 项目中的 mysql 操作吧。

## Docker 容器化 及 自动化运维脚本
下周实践
