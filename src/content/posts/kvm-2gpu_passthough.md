---
title: kvm双显卡直通
published: 2025-09-06
description: ''
image: ''
tags: []
category: ''
draft: true 
lang: ''
---

## IOMMU组

找到独显的group内容复制下来
``` bash
#!/bin/bash
shopt -s nullglob
for g in /sys/kernel/iommu_groups/*; do
    echo "IOMMU Group ${g##*/}:"
    for d in $g/devices/*; do
        echo -e "\t$(lspci -nns ${d##*/})"
    done;
done;
```
例如这样
（标记部分为硬件地址）
``` bash "10de:2786" "10de:22bc"
IOMMU Group 14:
        01:00.0 VGA compatible controller [0300]: NVIDIA Corporation AD104 [GeForce RTX 4070] [10de:2786] (rev a1)
        01:00.1 Audio device [0403]: NVIDIA Corporation AD104 High Definition Audio Controller [10de:22bc] (rev a1)
```