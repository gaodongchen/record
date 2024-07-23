+++
title = '纪念自己曾经的好朋友-VIM'
date = 2024-07-23T17:10:26+08:00
draft = false
categories = ['工具']
tags = ['历史', '工具']
+++

到北京的第二年，也是第二份工作，遇到了个清华毕业的技术型老板带我们做外派项目。
开发工作是在Linux系统中进行，每个人创建自己的开发环境，然后强制使用VIM进行编码。
从痛苦的适应阶段，到从容的使用阶段，再到后来如弹钢琴般丝滑的熟练阶段。每个阶段都注入相当多的精力去折腾。

对我而言，使用VIM是历史的一个必然过程。过去电脑性能低下，使用功能完善些的IDE时间长会卡顿。年轻的我写PHP代码也不需要提示，全靠脑子记忆（现在老了记不住了）。
如今与VIM不似那般如胶似漆了，日常的开发被```Visual Studio Code```所取代。在做服务器搭建、配置的时候偶尔使用几次，但这十多年使用的肌肉记忆却没有减退，依然虎虎生风😎。

**整理出自己最后的配置**（插件就免了）

```vim
set nobackup " 禁止备份 nobk
set autoread " 文件内容变更自动读取 ar
set number " 显示行号 nu
set showmatch " 显示括号匹配
set autoindent " 开启自动缩进 ai
set smartindent " 开启智能缩进 si
set incsearch " 开启实时搜索 is
set hlsearch " 开启高亮搜索 hls
set ignorecase " 搜索时大小写不敏感 ic
set wildmenu " 引导命令菜单
set showcmd " 显示命令 sc
set nocursorline " 关闭突出显示当前行 cul
set nocursorcolumn " 关闭突出显示当前列 cuc
set nocompatible " 关闭兼容模式 cp
set expandtab " 强制tab转换为空格 et
set tabstop=4 " 设置Tab长度为4空格 ts
set shiftwidth=4 " 设置自动缩进长度为4空格 sw
set laststatus=2 " 设置状态栏为2行 ls
set updatetime=100 " 刷新延迟时间，默认4000
set termguicolors " 开启24bit的颜色，开启这个颜色会更漂亮一些
colorscheme murphy " 指定配色主题
syntax enable
syntax on " 开启文件类型侦测
filetype plugin indent on " 启用自动补全
```

**结语**
> 人生很短，能陪伴自己很长的人或事物不多。珍惜当下的，不忘过去的，憧憬未来的。