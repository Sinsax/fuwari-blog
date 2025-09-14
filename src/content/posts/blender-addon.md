---
title: blender新版扩展(插件)指南
published: 2025-09-13
description: '插件的结构以及一些流程'
image: ''
tags: [blender,python,插件,扩展,指南]
category: '模型'
draft: true 
lang: ''
---

已有脚本可以直接跳到<a href="#quick">快速制作</a>

# 基础目录结构

:::Tip
使用git时建议新建.gitignore文件<br>
屏蔽__pycache__目录
:::

```txt "__init__.py" "blender_manifest.toml"
my_extension-0.0.1.zip
├─ __init__.py
├─ blender_manifest.toml
└─ (...)
# 以下两个是必需
blender_manifest.toml(清单)
__init__.py(初始化脚本)
```

---
# 代码结构

## blender_manifest.toml

最小结构:spoiler[**比较常用**]

<div style="display: flex;margin: 0 auto;align-items: center;">

<div style="width:50%">

```toml title="blender_manifest.toml"
schema_version = "1.0.0"
id = "my_example_extension"
version = "1.0.0"
name = "My Example Extension"
tagline = "This is another extension"
maintainer = "Developer name"

type = "add-on"

blender_version_min = "4.2.0"

license = ["SPDX:GPL-3.0-or-later",]
```
</div>
<div style="display: flex;margin: 0 auto;align-items: right;">
<pre>

schema_version 架构版本，一般都为1.0.0
id 扩展的唯一标识符
version 版本(自定)
name  扩展名称
tagline 扩展描述
最多64个字符,不能以标点符号结尾
maintainer 扩展的维护者

type 类型("add-on"/"theme")

blender_version_min 支持的最低版本

license  许可

</pre>
</div>

</div>


<details>
<summary>完整可选</summary>

显示的为必填内容，注释为可选
```toml title="blender_manifest.toml"
schema_version = "1.0.0"

# Example of manifest file for a Blender extension
# Change the values according to your extension
id = "my_example_extension"
version = "1.0.0"
name = "My Example Extension"
tagline = "This is another extension"
maintainer = "Developer name"
# Supported types: "add-on", "theme"
type = "add-on"

# # Optional: link to documentation, support, source files, etc
# website = "https://extensions.blender.org/add-ons/my-example-package/"

# # Optional: tag list defined by Blender and server, see:
# # https://docs.blender.org/manual/en/dev/advanced/extensions/tags.html
# tags = ["Animation", "Sequencer"]

blender_version_min = "4.2.0"
# # Optional: Blender version that the extension does not support, earlier versions are supported.
# # This can be omitted and defined later on the extensions platform if an issue is found.
# blender_version_max = "5.1.0"

# License conforming to https://spdx.org/licenses/ (use "SPDX: prefix)
# https://docs.blender.org/manual/en/dev/advanced/extensions/licenses.html
license = [
  "SPDX:GPL-3.0-or-later",
]
# # Optional: required by some licenses.
# copyright = [
#   "2002-2024 Developer Name",
#   "1998 Company Name",
# ]

# # Optional: list of supported platforms. If omitted, the extension will be available in all operating systems.
# platforms = ["windows-x64", "macos-arm64", "linux-x64"]
# # Other supported platforms: "windows-arm64", "macos-x64"

# # Optional: bundle 3rd party Python modules.
# # https://docs.blender.org/manual/en/dev/advanced/extensions/python_wheels.html
# wheels = [
#   "./wheels/hexdump-3.3-py3-none-any.whl",
#   "./wheels/jsmin-3.0.1-py3-none-any.whl",
# ]

# # Optional: add-ons can list which resources they will require:
# # * files (for access of any filesystem operations)
# # * network (for internet access)
# # * clipboard (to read and/or write the system clipboard)
# # * camera (to capture photos and videos)
# # * microphone (to capture audio)
# #
# # If using network, remember to also check `bpy.app.online_access`
# # https://docs.blender.org/manual/en/dev/advanced/extensions/addons.html#internet-access
# #
# # For each permission it is important to also specify the reason why it is required.
# # Keep this a single short sentence without a period (.) at the end.
# # For longer explanations use the documentation or detail page.
#
# [permissions]
# network = "Need to sync motion-capture data to server"
# files = "Import/export FBX from/to disk"
# clipboard = "Copy and paste bone transforms"

# # Optional: advanced build settings.
# # https://docs.blender.org/manual/en/dev/advanced/extensions/command_line_arguments.html#command-line-args-extension-build
# [build]
# # These are the default build excluded patterns.
# # You only need to edit them if you want different options.
# paths_exclude_pattern = [
#   "__pycache__/",
#   "/.git/",
#   "/*.zip",
# ]
```
</details>

## __init__.py

```python
bl_info = {
    "name": "addon name",
    "author": "author name",
    "description": "",
    "blender": (2, 80, 0),
    "version": (0, 0, 1),
    "location": "",
    "warning": "",
    "category": "Generic",
}


def register(): ...
    #注册Operator

def unregister(): ...
    #卸载Operator
```
---

# UI模板

# blender --command

# <p id="quick">快速制作</a>

```txt
my_extension-0.0.1.zip
├─ __init__.py
├─ blender_manifest.toml
└─ script.py(名称自选)
```

```python title="script.py"
import bpy

class script1(bpy.types.Operator):
    bl_idname = "object.script1"
    bl_label = "script1"
    bl_description = "第一个scrip"
    
    def execute(self, context):
        #这里放操作的内容
        return {'FINISHED'}

# 定义一个面板
class ShapekeyQuickPanel(bpy.types.Panel):
    bl_label = "addon_name"
    bl_idname = "OBJECT_PT_addon_name_panel"
    bl_space_type = 'VIEW_3D'
    bl_region_type = 'UI'
    bl_category = 'addon_name'
    
    def draw(self, context):
        layout = self.layout
        # 将之前定义的script1载入到面板上
        layout.operator("object.script1")
```

```python title="__init__.py"
bl_info = {
    "name": "addon_name",
    "author": "authorname",
    "blender": (2, 80, 0),
    "version": (0,1,1),
    "category": "Object",
}


import bpy
from . import script


# 注册和取消注册类
def register():
    bpy.utils.register_class(script.script1)



def unregister():
    bpy.utils.unregister_class(script.script1)

if __name__ == "__main__":
    register()

```