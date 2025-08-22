---
title: 图片转换为webp
published: 2025-08-23
description: '为了不被png卡死'
image: ''
tags: [图片压缩,webp]
category: 'Fuwari'
draft: false 
lang: ''
---

# Archlinux
## 安装
```bash
sudo pacman -S libwebp
```
## png/jpg转换webp

```bash 'png' 'jpg' 'images'

cwebp -q 80 image.png -o image.webp

# 批量
# 质量80%
for i in *.png; do cwebp -q 80 "$i" -o "${i%.*}.webp"; done
# 无损压缩 -lossless
for i in *.png; do cwebp -lossless "$i" -o "${i%.*}.webp"; done
```

## gif转换webp

```bash 'gif'

gif2webp -q 80 image.gif -o image.webp

# 批量
# 质量80%
for i in *.gif; do gif2webp -q 80 "$i" -o "${i%.*}.webp"; done
# 有损
for i in *.gif; do gif2webp -lossy -m 3 "$i" -o "${i%.*}.webp"; done
```

---
# python

## 安装Pillow
```bash
# pip
pip install Pillow

# archlinux
sudo pacman -S python-Pillow
```
## 代码参考
转换当前目录下的文件
```python title="webp.py"
from PIL import Image
import os
# 读取目录下的所有图片文件
def get_image_files():
    # 获取当前工作目录的路径
    directory = os.getcwd()
    image_files = []
    for filename in os.listdir(directory):
        if filename.lower().endswith(('.png', '.jpg', '.jpeg', '.bmp', '.gif')):
            image_files.append(os.path.join(directory, filename))
    return image_files
imagelist = get_image_files()
for image in imagelist:
    img = Image.open(image) 
    img.save(image.rsplit('.', 1)[0]+".webp", 'WEBP', lossless=True)
```

---
参考：[cwebp](https://developers.google.com/speed/webp/docs/using?hl=zh-cn)
