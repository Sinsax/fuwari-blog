---
title: 模型制作流程(vroid素体)
published: 2025-08-24
description: 'vroid素体+blender'
image: ''
tags: [模型,流程,blender,mmd,arkit,vrm,vroid]
category: '模型'
draft: false 
lang: ''
---

# 1. 素体（决定了大部分的形态键预设）

## vroid
- **vroid**捏大致脸型和眼型（可后续修改）

- **反复**—在blender内检查是否满意

- vroid导出时去掉 **去除透明材质网格** 的勾选，导出为vrm模型

## blender
- 导入blender:
- blender安装[vrm插件](https://github.com/saturday06/VRM-Addon-for-Blender)(4.5版本可直接在扩展中安装)，并导入

<!-- **vroid2pmx**--要求骨骼名不变（Tpose->Apose，angle:35°） -->

---

# 2. 面捕形态键(Arkit)

- 手搓

    - [https://hinzka.hatenablog.com/entry/2020/06/15/072929](https://hinzka.hatenablog.com/entry/2020/06/15/072929)

    - [【努力一下人物建模】10-手搓完美同步，尊嘟假嘟？](https://www.bilibili.com/video/BV1wT421i7T7/?spm_id_from=333.999.list.card_archive.click&vd_source=464747023d65135382bc51c6e3680fc3)

:::tip
将脸部用unity转化成arkit
:::
- Hana_Tools

    <details>
    <summary>参考教程</summary>
    <p>

    [【3D化教學】3D模型精細臉部動補完整攻略，超好用動補軟體與工具介紹，使用HANA Tool快速設置52 Blendshapes！](https://www.youtube.com/watch?v=Ex_CCxz7gK4)

    [【Vroid面捕教程】最简单的面捕/动捕方案（软件见简介）](https://www.bilibili.com/video/BV1Gx4y177CP)
    </p>
    </detials>
    V4（VRM0.0）：

    [https://kuniyan.booth.pm/items/2604269](https://kuniyan.booth.pm/items/2604269)

    - 推荐参数

        ・Unity2020.3.13f1(64bit) 

        ・UniVRM0.98.0 

        ---

        v5（VRM1.0）这阶段好像不太受用

        [https://kuniyan.booth.pm/items/4607357](https://kuniyan.booth.pm/items/4607357)

        - 推荐参数

            ・Unity2020.3.13f1(64bit) 

            ・VRM0.108.0

        但是我他妈买错了

---

# 3. 转换为mmd格式//可后续转换

用vrm2pmx转为pmx模型

- 可选  T-POSE（为了建模习惯）

    1. blender2.93，cat插件

    2. pmxediter转换

    3. 用写的脚本转换

**素体完成**🎉


---

# 4. 建模


:::tip
如果因为骨骼的命名问题，无法镜像。

需要cats应用"sysmmetruze VRoid Bone Names on X-Axia"
:::
**要时刻保证模型的对称性(主要是面部)**



### ~~建模过程skip~~



绑定一定要起名

材质初步只有贴图

此后是pe和blender来回的问题了（不过要避免，会出错）


- 配合脚本

    - 将arkit表情转为mmd的

    - 材质转换

    - uv转换？

    
---

# 5. mmd处理

> 一些mmd格式参考

## 显示杂

### 1.骨骼列表
<details>
<summary>点击展开</summary>
<p>

- ROOT

    - 操作中心

- 表情

- センター

    - 全ての親

    - センター

    - グルーブ

- IK

    - 足ＩＫ

    - つま先ＩＫ

- 体（上）

    - 上半身

    - 首

    - 頭

    - 両目

    - 右目

    - 左目

- 腕

    - 右肩

    - 右手首

    - 右朊捩

    - 右手捩

- 指

    - 略

- 体(下)

    - 下半身

- 足

    - 右足

    - 右ひざ

    - 右足首

    - 右足D

    - 右ひざD 

    - 右足首 D

    - 右足先 EX

    - 右つま先

- 物理

    - 略，可分组
</p></details>



### 2.注释 

<details open=true>
<p>
ModelName : gugu

Author : Sinsa

Contact Information :https://space.bilibili.com/1627170029
</p></details>

### 3.材质

<details open=true>
<p>

- 扩散色：0.8

- 反射色：0

- 环境色：0.6

- 反透射率：1

- 反射强度：5
</p></details>

## mmd表情适配

[https://github.com/Sinsax/mmd-facial-expression](https://github.com/Sinsax/mmd-facial-expression)

**todo**

---

## 裙子物理

横16纵8

**参考模型:兰若**

<details open=true>
<p>

- 纵关节参数：

    - 移动距离：0厘米

    - 旋转角度：80度

    - 移动距离：0厘米

    - 回转角度：10度

    横关节参数：

    - 移动距离：0.1~1厘米

    - 旋转角度：1度

    - 移动距离：40~0厘米

    - 回转角度：0度

</p></details>

---


:::important
检查:材质顺序，颜色，双面，透明

裙子曲面物理效果

添加必需骨
:::

**pmx模型基本完成**
    
---

# 导出后调试

todo





