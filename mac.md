# Mac学习笔记

#### Homebrew学习笔记
```shell
安装包
`brew install pyenv`  

更新包
`brew update && brew upgrade pyenv`
```

#### 使用软件：Snap
给自己的常用app设置呼出快捷键。

#### 使用软件：Seil
将右边的command键，映射为ctrl键的功能。  
互换capslock、esc按键的功能。

#### 软件卡死，怎么强制退出：
Command + option + shift + esc 按住一两秒就退出了

#### 重装系统方法：
开机的时候按住option键不放。

#### 没有权限操作根目录下的文件，如/usr/bin/vim:
重新开机，按住command + r 不放。在实用工具中打开命令行终端，输入：  
`csrutil disable`  
`reboot`

#### 隐藏系统自带的vim版本，用homebrew安装新的vim版本。
`brew install vim --override-system-vim`  
修改.zshrc脚本，增加一行 `alias="/usr/local/bin/vim"`  
`mv usr/bin/vim usr/bin/vim73`