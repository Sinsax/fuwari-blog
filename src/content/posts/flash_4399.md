---
title: archlinux中玩原flash游戏
published: 2026-01-21
description: ''
image: ''
tags: [linux,flash]
category: 'linux'
draft: false
lang: ''
---
# 玩4399
想玩4399了，但是ruffle不能使用在国内特供的flash版本上

windows有celbrowser,但linux的版本暂没找到

此处用的52版本firefox+aur中的flashplugin

# 安装

flash插件
```bash
paru flashplugin
#或
yay flashplugin
```
firefox 52版本
```
https://ftp.mozilla.org/pub/firefox/releases/52.0esr/
```

# 设置更新

此处firefox要特殊处理一下防止自动更新导致不能使用flash

## 解压在合适地方并且将文件夹设置为只读
## firefox内设置
1. 右上角菜单Preferences
2. Advanced->Update
3. 选择 Never check for updates（永不检查更新）
4. 也可以选择关闭automaticallyupdate: search engines


