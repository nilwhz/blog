# SublimeText学习笔记

#### 序列号
注意：该序列号对3095版本适用。  
```
----- BEGIN LICENSE -----
Michael Barnes
Single User License
EA7E-821385
8A353C41 872A0D5C DF9B2950 AFF6F667
C458EA6D 8EA3C286 98D1D650 131A97AB
AA919AEC EF20E143 B361B1E7 4C8B7F04
B085E65E 2F5F5360 8489D422 FB8FC1AA
93F6323C FD7F7544 3F39C318 D95E6480
FCCC7561 8A4A1741 68FA4223 ADCEDE07
200C25BE DBBC4855 C4CFB774 C5EC138C
0FEC1CEF D9DCECEC D3A5DAD1 01316C36
------ END LICENSE ------
```

#### 安装方法
- 官网下载SublimeText 3 Build最新版本（或者3095版本）。
- 安装启动，输入序列号。
- 打开终端并输入：
```
cd Library/Application\ Support/Sublime\ Text\ 3/Packages/User
git git@github.com:winux404/subl_config.git
mv subl_config/* .
rm -rf subl_config
```
- 在SublimeText中使用ctrl + `打开终端面板，安装Package Control。  
Package Control安装过程中根据User目录中的配置文件，将自动安装所有插件以及你自己的所有个性化设置。

#### 保存SublimeText的所有自定义配置
用户的所有配置文件会被保存到User文件夹中。  
在菜单栏中选择：SublimeText - Preferences - Browse Packages 可以看到User文件夹。

#### 自定义SublimeText快捷键
1. 快捷键ctrl + `  调出命令行窗口并输入：sublime.log_commands(True)
2. 执行相关操作，在命令行窗口中就会记录下相关操作的命令名和参数。
3. 参考Key Bindings - Default 中的配置写法，在key Bindings - User中进行配置。

#### 自定义snippet
在菜单栏中选择：tools - new snippet  
创建完成的snippet会被保存到User文件夹中。

#### 常用快捷键
- 通用
```
ctrl + `  调出控制台面板

command + shift + p  调出命令面板
在这里面，可以输入各种命令，对于一些不常用的快捷键，可以使用这种方式实现。

command + K + B   sidebar隐藏显示切换
```

- 查找替换
```
command + P      Go to anything
输入文件名，自动定位到该文件
： 定位到第几行
@  定位到函数
#  定位到字符
可以组合使用

command + f  文件内查找
command + alt + f 文件内查找和替换
进入command + f或者command + alt + f之后，继续执行：
—————— 选择或者替换单个单词：
command + g  选择下一个单词
command + shift + g   选择上一个单词
command + alt + e  替换该单词
—————— 选择或者替换所有单词：
alt + 回车    选中所有单词
ctrl + alt + 回车   替换所有单词

ctrl + 减号    退回跳转之前的文件光标位置
ctrl + shift + 减号    如果ctrl + 减号   多按了一次，可执行它的相反操作。
```

- 光标选中
```
多点模式：
command + d   选中该单词
command + ctrl + g  全选该单词
按住alt，拖动光标。
按住command，单击光标。
选中文本后，command + shift + l  进入多点编辑模式。
esc   退出多点模式。

command + L     选中一行
command + shift + J     以缩进层级为依据一层一层向外选中
command + shift + L     将选中的行分割成多点模式
ctrl + shift + 上下箭头     想上（下）一行一行选中

ctrl + m 在括号内移动
ctrl + shift + m 选中括号内的内容
```

- 编辑
```
command + enter  向下插入一行
command + shift + enter  向上插入一行

command + ctrl + 上箭头  与上一行互换
command + ctrl + 下箭头  与下一行互换

command + shift + d  复制粘贴当前行到下一行

command + j     拼接行

ctrl + k    从光标开始的地方删除到行尾
ctrl + shift + k    删除当前行整行

ctrl + t    相邻字母互换位置

command + alt + t   插入特殊符号（好酷的功能啊）
```
