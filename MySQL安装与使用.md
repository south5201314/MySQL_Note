[TOC]

# MySQL安装

## 下载

* http://dev.mysql.com/downloads/mysql

## 配置环境变量

* 在安装MySQL时，环境变量没有配置手动，需要手动去设置。
* 把安装目录下的bin目录配置到环境变量。

## MySQL服务

* 方式一：通过计算机管理方式
  * 右击计算机—管理—服务—启动或停止MySQL服务

* 方式二：通过命令行方式
  * 启动：net start mysql(服务名)
  * 停止：net stop mysql(服务名)

# MySQL使用

## 登录和退出

* 登录：
  * mysql -h 主机名 -u 用户名 -p 密码
  * mysql -h localhost - u 用户名 -p 密码(连接本地数据库)

* 退出
  * exit

## 常用数据库命令

| 命令                         | 描述                         |
| ---------------------------- | ---------------------------- |
| SHOW DATABASES;              | 查看mysql中的所有数据库      |
| USE 数据库名;                | 使用数据库                   |
| CREATE DATABASE 数据库名;    | 新建数据库                   |
| SHOW TABLES [FROM 数据库名]; | 查看指定(或当前)数据库中的表 |
| DESC 表名                    | 查看表的结构                 |
| DROP TABLE 表名              | 删除表                       |

