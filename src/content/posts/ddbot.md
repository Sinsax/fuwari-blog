---
title: DDBOT配置备忘
published: 2025-08-21
description: '每次都忘记怎么弄，遂记录'
image: ''
tags: [DDbot,QQ,NapCat]
category: 'QQ'
draft: false 
lang: ''
---
:::tip
环境为linux服务器
:::
# 安装1panel(可选)
方便管理docker和文件
```bash
bash -c "$(curl -sSL https://resource.fit2cloud.com/1panel/package/v2/quick_start.sh)"
```

---

# DDBOT
::github{repo="cnxysoft/DDBOT-WSa"}

## 安装

下载，然后解压在一个目录里

:::tip
<?>尖括号是缺省参数
:::
> systemd可持续运行
```bash 
#ddbot.sh
#!/bin/sh
cd /<filepath>/ddbot
./DDBOT-WSa
```

```bash
#ddbot.service
[Unit]
Description=
Documentation=
After=network.target
Wants=
Requires=

[Service]
Restart=on-failure
RestartSec=10s
StartLimitIntervalSec=300
StartLimitBurst=5
ExecStart=/<filepath>/ddbot.sh
ExecStop=
ExecReload=/<filepath>/ddbot.sh
Type=simple

[Install]
WantedBy=multi-user.target
```

放置并运行
```bash
# 移动文件
cp ddbot.service /etc/systemd/system/ddbot.service
# 启用开机自启
systemctl enable ddbot
# 启动服务
systemctl start ddbot
```
后续查看运行状态
```bash
systemctl status ddbot
```


## 配置
用bilibili扫一下ddbot目录下的b站二维码图片

---

# Napcat
::github{repo="NapNeko/NapCat-Docker"}
## 安装(二选一)

:::tip
使用1panel部署时，注意网络设置为host
:::

### Napcat docker

```bash
docker run -d \
-e NAPCAT_GID=$(id -g) \
-e NAPCAT_UID=$(id -u) \
-p 3000:3000 \
-p 3001:3001 \
-p 6099:6099 \
--name napcat \
--restart=always \
mlikiowa/napcat-docker:latest
```
### docker-compose
```bash
# docker-compose.yml
version: "3"
services:
    napcat:
        environment:
            - NAPCAT_UID=${NAPCAT_UID}
            - NAPCAT_GID=${NAPCAT_GID}
        ports:
            - 3000:3000
            - 3001:3001
            - 6099:6099
        container_name: napcat
        network_mode: bridge
        restart: always
        image: mlikiowa/napcat-docker:latest
```
## 链接Napcat
网络配置 -- 新建Websocket客户端

记得勾选`开启debug`
```
url:
ws://127.0.0.1:15630/ws
```
:::tip
在猫猫日志中可以看到是否有连接错误
:::

*至此链接成功了*🎉
---

---

# 配置机器人
> 在qq向小号发送消息
>
一些常用的指令
```bash
# 指定管理员
/whosyourdaddy
/watch UID
/watch -t news UID
/config at_all --site bilibili UID on
/config title_notify --site bilibili UID on

# 直播
/watch -g <group> <live>
# 动态
/watch -g <group> -t news <live>
# @全体
/config -g <group> at_all --site bilibili <live> on
# 标题修改
/config -g <group> title_notify --site bilibili <live> on
```
---
参考内容：[DDBOT](https://ddbot.songlist.icu/),[NapNeko](https://napneko.github.io/),[napcat-1panel](https://github.com/Fahaxikiii/napcat-1panel)