---
title: 网易云音乐歌名提取
published: 2025-11-05
description: ''
image: ''
tags: ["网易云音乐","obs"]
category: 'linux'
draft: false 
lang: ''
---
# 原因
起因是最近用linux直播，然后脑子有问题

# 前置需要:
- wine版本的网易云音乐
- xdotool
# 使用方式
- 保存到合适的地方
- 运行后会将提取的歌名输出到title.txt中
- 在obs内选择文字即可，换歌时他会自动切换
- 如果没找到对应程序次数过多他会自动退出
# 具体代码
```python title="music_get.py"
import os
import subprocess
import time
def xdotool(process,target_id=""):
    try:
        if process == "target_id":
            command = "xdotool search --classname cloudmusic.exe".split(" ")
            target_id = subprocess.run(command, capture_output=True, text=True, check=True).stdout.strip().split("\n")[0]
            return target_id
    except Exception as e:
        print("未找到网易云")
        return ""
    # end try
    if process == "wm_name":
        command = f"xprop -id {target_id} WM_NAME".split(" ")
        wm_name = subprocess.run(command, capture_output=True, text=True, check=True).stdout.strip().split('=', 1)[1].strip().strip('"')
        return wm_name
    # end try

output_file = "title.txt"
print(f"结果将实时保存到: {output_file}")
wm_name =""
exitcount = 0
while True:
    if exitcount == 5:
        break
    try:
        temp = xdotool("wm_name",target_id)
        if wm_name != temp:
            wm_name = temp
            with open(output_file, 'w', encoding='utf-8') as f:
                f.write(wm_name)
            print(f"歌名:{wm_name}")
    except Exception as e:
        # 提取第一个符合条件的 ID
        target_id = xdotool("target_id")
        # 检测是否无法检测到程序
        if target_id=="":
            if exitcount == 0:  
                # 防止多次写入 
                with open(output_file, 'w', encoding='utf-8') as f:
                    f.write(target_id)
            exitcount = exitcount+1
    # 间隔一秒
    time.sleep(1)
```