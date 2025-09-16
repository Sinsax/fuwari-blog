---
title: 使用ssh链接github的一些问题
published: 2025-09-16
description: ''
image: ''
tags: []
category: ''
draft: false 
lang: ''
---

起因是这个
```bash
ssh: connect to host github.com port 22: Connection refused fatal: Could not read from remote repository. Please make sure you have the correct access rights and the repository exists.
```
原因可能是我更新了win11

# 解决

这里有几种解决方法，都可以试一下
## 重新生成ssh-gen
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```
在github->Settings->SSH keys重新new一个
记得删除之前的sshgen


## 重新验证github

```bash
vi ~/.ssh/config
```

```txt title ="config"
Host github.com
 Hostname ssh.github.com
 Port 443
```

```bash
ssh -T git@github.com
```
## windows服务
启用OpenSSH Authentication Agent，并设为自动
```bash
ssh-add ~/.ssh/id_ed25519
```