### Neovim

### 下载neovim

```bash
brew install neovim
```



### 背景：Lua

**Lua** 是一个小巧的脚本语言。作者是巴西人。该语言的设计目的是为了嵌入应用程序中，从而为应用程序提供灵活的扩展和定制功能。

Lua 由标准 C 编写而成，代码简洁优美，几乎在所有操作系统和平台上都可以编译，运行。

Lua 脚本可以很容易的被 C/C++ 代码调用，也可以反过来调用 C/C++ 的函数，这使得 Lua 在应用程序中可以被广泛应用。不仅仅作为扩展脚本，也可以作为普通的配置文件，代替 XML,Ini 等文件格式，并且更容易理解和维护。



#### lua annotation

Lua中有两种注释：行注释和块注释。
行注释以“--”开头，可以注释这一行后面的内容。
块注释以“--[[”开始，以“--]]”结尾，可以注释这个范围内的整个内容；块注释可以注释多行内容。
下面是一个示例：

```lua
print("hello")
-- 这是行注释
--[[
这是块注释，
块注释可以
注释多行！
--]]
```







### vim syntax

```lua
-- source the init.lua again
:so


```



### All the commands used to customize the neovim

#### terminal commands

```bash
mkdir .config/nvim
# 创建空文件
touch init.lua 
mkdir .config/
```

#### init.lua

```bash
vim.opt.relativenumber = true
vim.opt.number = true
```







### Neovim IDE from Scratch 

参考youtube视频

https://www.youtube.com/watch?v=ctH-a-1eUME&list=PLhoH5vyxr6Qq41NFL4GvhFp-WLd5xzIzZ

github仓库：

https://github.com/LunarVim/Neovim-from-scratch/tree/01-options

```bash
➜  ~ git clone git@github.com:ChristianChiarulli/Neovim-from-scratch.git ~/.config/nvim
```

这是使用vim编辑的第一行文字



### neovim as an IDE for R

How to use Neovim or VIM Editor as an IDE for R
