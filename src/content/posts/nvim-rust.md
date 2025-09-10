---
title: 给neovim安装lazyvim并启用rust支持
published: 2025-09-10
description: ''
image: ''
tags: [neovim,lazyvim,rust]
category: 'linux'
draft: false 
lang: ''
---
基于archlinux配置

# 安装neovim&lazyvim
```bash
# archlinux
sudo pacman -Sy neovim

git clone https://github.com/LazyVim/starter ~/.config/nvim

rm -rf ~/.config/nvim/.git

nvim
# 等待安装完成
```

# 安装rust支持
```bash "lang.rust"
#在nvim中输入命令
:LazyExtras
#找到 lang.rust 摁x启用
```

# 添加rust-analyzer
在option.lua中添加

```lua
vim.g.lazyvim_rust_diagnostics = "rust-analyzer"
```

```tree "options.lua"
~/.config/nvim
├── lua
│   ├── config
│   │   ├── autocmds.lua
│   │   ├── keymaps.lua
│   │   ├── lazy.lua
│   │   └── options.lua
│   └── plugins
│       ├── spec1.lua
│       ├── **
│       └── spec2.lua
└── init.lua
```


# neovim操作
**和vim的操作同理**

```hack

普通模式(Normal Mode):
    進入Neovim 後即處於此模式，主要用於移動游標、複製、剪下、貼上及其他命令。
按下 i 進入插入模式。
按下 Esc 從插入模式、視覺模式等返回普通模式。
按下 v 進入視覺模式(Visual Mode)，用於選取文字。
按下 y 複製選取的文字。
按下 x 或 c 剪下選取的文字。
按下 p 貼上剪下或複製的文字。
按下 u 復原（撤銷）上一步操作。
按下 / 並輸入文字後按回車，可在文件中搜尋該文字。
按下 Ctrl + F 可進行翻頁。
0 將游標移動到行首，$ 將游標移動到行尾。

插入模式(Insert Mode)：
    用於輸入和編輯文字。
從普通模式按下 i 即可進入。
命令行模式(Command Mode)：
    用於執行更複雜的命令，如保存和退出。
在普通模式下按下 : 
    進入命令行模式。
輸入 q 退出，w 保存，wq 保存並退出。
```

# 参考
[lazyvim-Installation](https://www.lazyvim.org/installation)

[lazyvim-rust](https://www.lazyvim.org/extras/lang/rust)
