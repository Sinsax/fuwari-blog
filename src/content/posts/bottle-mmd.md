---
title: linux内使用bottle启动MMD和PE
published: 2025-08-26
description: ''
image: ''
tags: [wine,mmd,bottle]
category: '模型'
draft: false 
lang: ''
---

对此篇文档的一个笔记:
> [嘗試在Linux跑MikuMikuDance和PMX Editor建模軟體](https://ivonblog.com/posts/mikumikudance-linux/)

# 安装Bottles

右上角➕新建bottle

类别游戏,soda9.0.1(可选最新版本)
> 这里我用的是cachyos自带的版本

- 安装依赖
    - cjkfonts
    - vcredist2005
    - vcredist2008
    - vcredist2010
    - vcredist2013
    - devenum
    - quartz
    - d3dx9
    - qcap
    - qedit
    - d3dcompiler_43
    - gdiplus
    - directshow

设置语言为**Japanese**

新建环境变量

    LANG=ja_JP.UTF-8

# PE可共用这个bottle
导入模型可能需要从菜单，不能直接拖入