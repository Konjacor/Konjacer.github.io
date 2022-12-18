---
title: Linux常用操作
date: 2022-09-14 11:18:47
tags: [linux]
---

<meta name="referrer" content="no-referrer"/>

# 常用命令

## 解压目标到另外一个文件夹

- **tar -zxvf 文件名 -C 文件夹路径**，一定要加-C来说明要解压到指定目录

- 示例：**tar -zxvf redis-6.0.6.tar.gz -C ../redis**

## 永久关闭防火墙

- **systemctl disable firewalld**

## 查找含有某字符串的进程

- **ps -ef | grep redis**

## CentOS中暂时修改gcc的版本

- 使用这个命令之前需要进行安装操作：

  ```shell
  yum install centos-release-scl scl-utils-build #SCL(Software Collections)是一个CentOS/RHEL Linux平台的软件多版本共存解决方案，为RHEL/CentOS  Linux用户提供一种方便、安全地安装和使用应用程序和运行时环境的多个版本的方式，同时避免把系统搞乱。
  yum install -y devtoolset-8-toolchain #安装工具集
  ```

- 然后使用**scl enable devtoolset-8 bash**会将gcc的版本暂时设置为8.*，在终端会话结束时恢复。
