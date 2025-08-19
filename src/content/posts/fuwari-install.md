---
title: Fuwari安装&使用
published: 2025-08-18
description: '使用github page部署'
image: ''
tags: [指南,Fuwari]
category: 'Fuwari'
draft: false 
lang: ''
---
本文档为使用github page部署的指南
# 安装fuwari（二选一）
## 1.直接fork原仓库
::github{repo="saicaca/fuwari"}

## 2，用pnpm安装
```bash
pnpm create fuwari@latest
```
按命令输出需求依次输入项目名称，网站名称，副标题，语言
```bash
✔ Please enter the project name: 输入项目名称
✔ Please enter the site title: 输入网站名称
✔ Please enter the site subtitle: 输入副标题
✔ Please select the language of the site. zh_CN
✔ Install Dependencies? Yes
✔ Initialize Git? Yes
```


# 配置fuwari
:::tip
用pnpm安装时，基础网站信息会提前更改
:::

## 手动设置网站信息``src/config.ts``

网站基本信息在``export const siteConfig: SiteConfig:{``
``` ts "网站标题" "副标题"
title: 网站标题,
subtitle: 副标题,
lang: "zh_CN"
```

横幅
```ts "banner.png"
banner: {
    enable: false,
    src: "assets/images/banner.png", 
}
```

头像内容在``export const profileConfig: ProfileConfig = {``
```ts "demo-avatar.png" "Lorem Ipsum"
avatar: "assets/images/demo-avatar.png",
name: "Lorem Ipsum",
```
图片相关按照目录路径输入


## 设置``astro.config.mjs``
项目根目录下打开``astro.config.mjs``
设置
```mjs "https://fuwari.vercel.app/" ""/""
// https://astro.build/config
export default defineConfig({
	site: "https://fuwari.vercel.app/",
	base: "/",
	trailingSlash: "always",
)}
```
按github项目名分两种情况
1. 名为``username.github.io``

base可注释掉
```mjs "base:"/""
site:"https://username.github.io"
base:"/"
```
2. 其他名称

项目名例如 ``newpost``
```mjs "base:"/newpost""
site:"https://username.github.io"
base:"/newpost"
```

# github action 设置
## 关闭github已有action
:::important
不关会一直报错给你发邮件
:::
在github项目页面的Settings > Pages 中

将Build and deployment即生成和部署的方式改为

GitHub Action
## 配置提交代码即运行action
:::tip
若已有此文件可跳过
:::
在``.github/workflows``目录下新建``build.yml``

```yml
name: Deploy to GitHub Pages

on:
  # Trigger the workflow every time you push to the `main` branch
  # Using a different branch name? Replace `main` with your branch’s name
  push:
    branches: [ main ]
  # Allows you to run this workflow manually from the Actions tab on GitHub.
  workflow_dispatch:

# Allow this job to clone the repo and create a page deployment
permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout your repository using git
        uses: actions/checkout@v4
      - name: Install, build, and upload your site
        uses: withastro/action@v2
        with:
          # path: . # The root location of your Astro project inside the repository. (optional)
          # node-version: 20 # The specific version of Node that should be used to build your site. Defaults to 20. (optional)
          package-manager: pnpm@latest # The Node package manager that should be used to install dependencies and build your site. Automatically detected based on your lockfile. (optional)

  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

# 使用
## 本地运行并参考效果
```bash
#安装依赖项
pnpm install

#运行
pnpm run dev
pnpm dev

```


## 新建post

```bash 
pnpm new-post 名称
```

若需要插入图片，新建文件夹并改名为index.md

>* `newpost.md`

>- newpost
>   - `index.md`
>   - `picture.jpg`

或
>- newpost
>   - `index.md`
>   - image
>       - `picture.jpg`


## 图片追加
```ts
//md文件内添加
![](image/chibiysyk.gif)
```

---
参考来源：
[Fuwari](https://github.com/saicaca/fuwari),
[Astro doc](https://docs.astro.build/en/getting-started/),
[Markdown 基本语法](https://markdown.com.cn/basic-syntax/)
