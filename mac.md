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

#### 用TimeMachine恢复系统时出错，找不到系统磁盘，且用磁盘工具无法重新格式化抹掉，解决办法。
```shell
进入命令终端，输入：
diskutil cs list

在输入以上命令后，在命令行显示的信息中找到：Logical Volume Group，它后面的字母就是你电脑主硬盘的UUID。
输入以下命令：
diskutil cs delete UUID(将UUID替换为找到的字母信息)

这样，你自己的主硬盘就被重置了，随后再进入硬盘工具，就会发现已经可以重新抹掉格式化了，然后再恢复系统即可。
```