# Linux学习笔记

## 终端快捷键
```shell
ctrl + a    移动到行首
ctrl + e    移动到行尾

esc + f     按单词，向前移动。
esc + b     按单词，向后移动。

ctrl + w    剪切光标前的单词
ctrl + k    剪切光标后的所有文字
ctrl + u    剪切当前行
ctrl + y    粘贴
ctrl + l    清屏

ctrl + r    检索历史命令，继续按ctrl + r可以继续向前检索，按esc可退出检索。
ctrl + c    终止当前任务
ctrl + z    将当前任务放到后台执行，使用fg可以恢复。

command + 回车    item快捷键，全屏。
command + d     item快捷键，左右分屏。
command + shift + d     item快捷键，上下分屏。
```

## 基本命令
```bash
mkdir -p code/memeda/hah/blue
建立多层次文件夹方法  
使用 -p 参数，可以建立多层次的文件夹，意味着hah这些文件夹原来可以是不存在的。
```

## 用户管理
```bash
whoami 查看当前用户名  
hostname 查看当前主机名
```

`passwd vwhz`  
修改vwhz用户的密码  
如果忘记了该用户的密码，可以使用root超级用户修改，这时候输入root密码即可。

`-rwxr-r---`  
第一位字符-表示文件，d表示文件夹目录，l表示链接  
后面的9个字符，每3个为一组，分别表示：所属用户、用户所属组用户、其它用户。  
r表示读权限  
w表示写权限  
x表示执行权限  
-表示没有权限  
r   4  
w   2  
x   1  
`-   0  `  
`chomd 700 tt.py`   表示将tt.py的权限改为 -rwx------  
即当前用户的权限为r、w、x，而所属组用户、其它用户都没有任何权限。  

还有一种修改权限的方式：  
`chmod -x code`  
对code文件夹减少执行权限  
`chmod +x code`  
对code文件夹增加执行权限  
注意：这种方式只能对当前用户有效，即只能改前3位的rwx属性。对group、world的用户无效。

## 文件系统
三种创建文件的方法：  
`touch tt.py`  
`> tt.py`  
`vim tt.py`

`> test.js`  清空文件  

0、1、2分别表示 标准输入 标准输出 错误输出  
重定向的使用：  
`cat code/tt.py > foo`   将标准输出重定向到foo文件，而不是直接在屏幕显示出来  
`cat code/test.py >> foo`   以追加的方式将标准输出重定向到foo文件  
`ls memeda 2> foo`    将错误输出重定向到文件foo  
`ls memeda &> foo`    将标准输出、错误输出都重定向到foo文件

## 进程操作
`nohup python -u test.py &`  
让python test.py命令在后台执行，并且退出终端并不会结束它的执行。  
参数 -u 的作用是，取消python的缓存，让输出到nohup.out文件的东西立即显示出来。  
`ps -ef | grep python test.py`  
查看nohup命令的uid。   
注意，对于nohup命令执行的进程，使用jobs显示的pid来kill是无法杀死。  
`kill 28146`  
杀死该进程  

`python test.py > log.txt &`  
让test.py程序在后台执行，并将标准输出的内容重定向到log.txt文件

`jobs`  检查后台执行的程序进程

`kill %1`  杀死进程

`fg %1`  将进程放到前台

`bg %1`  将进程放到后台

## 压缩命令
#### .zip格式
`zip -r xx.zip xx/`  压缩  
`uzip xx.zip`  解压  

#### .tar.gz格式
`tar -zcvf xx.tar.gz xx/`  压缩  
`tar -zxvf xx.tar.gz`  解压  
tar本身只做归档工作，并不负责压缩。  
一般是先用tar归档好文件后，再用gzip或者bzip2命令进行压缩。  
但这里我们对tar的使用方式，相当于是结合了tar命令、gzip命令一起使用。  
linux系统下压缩工作用得最多的就是gzip命令，其次才是bzip2。  
`tar -ztvf xx.tar.gz`  只显示，不解压。    
-t显示xx.tar.gz压缩文件中包含哪些文件，但是并不解压出来。  

#### .gz格式:
`gzip xx.tar`  压缩  
`gunzip xx.tar.gz`  解压  
`zcat xx.tar.gz`  只显示，不解压。  

#### .tar.bz2格式
`tar -jcvf xx.tar.bz2 xx/`  压缩  
`tar -jxvf xx.tar.bz2`  解压  
这里我们对tar的使用方式，相当于是结合了tar命令、bzip2命令一起使用。  

#### .bz2格式：
`bzip2 xx.tar`  压缩  
`bunzip2 xx.tar.bz2` 解压   
`bzcat xx.tar.bz2`  只显示，不解压

## 网络命令
#### 检查系统端口号监听情况
```shell
例如：检查3306端口的监听情况

输入以下命令：
sudo lsof -i :3306

如果mysql进程正在监听该端口，结果可能是：
COMMAND PID   USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
mysqld   73 _mysql   21u  IPv6 0xbb497661971c241d      0t0  TCP *:mysql (LISTEN)

如果该端口没有被监听，则不会有信息显示在终端里。

由上图显示，我们知道该进程的PID是73，所以我们可以杀掉它，输入以下命令：
sudo kill -9 73
这样一来，该端口的监听就结束了。
```

#### 测试网络
`ifconfig`  查看本机ip信息  

`ping www.baidu.com`  
从本地主机向目标服务器发送一个特殊的包，通过服务器返回过来的数据，可以判断到该服务器的网络状况。  
注意：有些服务器禁止了ping访问。

`curl -x http://183.131.151.208:80 -L http://www.8kana.com`
用代理ip去ping指定网站，测试该代理是否可用。

#### ssh命令远程登录计算机
`sudo apt-get install openssh-server`  在ubuntu上安装ssh服务端  

`ssh vwhz@192.168.166.139`  mac主机通过ssh远程登录ubuntu主机  

`ssh vwhz@192.168.1.105`  通过ubuntu虚拟机远程登录mac主机  

> 注意：使用ssh登录的时候，如果有端口号  
ssh -p 54321 vwhz@192.168.166.139  
-p紧跟在ssh后，且p为小写  

> 如果在本机的/etc/hosts文件中写入了配置，如：  
192.168.166.139 zz  
则可以通过域名zz，而不是ip地址来远程登录  
ssh vwhz@zz

> 如果本机用户和远程主机用户是一个的话，则可以省略域名前面的东东  
ssh zz

`sudo su 或者 sudo -s`  在ubuntu上切换到root用户  
`su vwhz 或者 exit`  切换回vwhz用户

#### scp命令下载和上传文件
`scp code/foo vwhz@192.168.166.139:/home/vwhz`  上传文件  

`scp vwhz@192.168.166.139:/home/vwhz/foo  ~/code/foo_down`  下载文件

> 注意，使用scp的时候，如果有端口号：  
scp -P 54321 code/foo vwhz@192.168.166.139:/home/vwhz  
scp -P 54321 vwhz@192.168.166.139:/home/vwhz/foo  ~/code/foo_down  
1、不论是上传还是下载文件，端口号的指定都必须紧跟在scp命令后。  
2、scp命令只能传输文件，而不能传输文件夹。  
3、-P是大写

#### 同步文件
`rsync -r vwhz@192.168.1.105:/Users/vwhz/playground ./`  
同步远程主机192.168.1.105上的playground文件夹中的所有数据到当前主机的./目录下。

> 注意：  
1、如果本机用户名和远程主机的用户名是一样的话，可以省略@前的用户名。  
2、如果只打算同步到home目录下，则可以省略host冒号后面的路径，但是冒号不能省略。  
rsync -r code 192.168.166.141:  
将本机上的code文件夹同步到远程主机的home目录下  
3、使用 -av 参数可以查看具体传输信息  
4、如果想要同步本机code目录下的所有文件到远程主机上的play目录下：  
rsync -r code/ 192.168.166.141:/home/vhwz/play  
code后面的/不能省略，否则code整个文件夹都同步到play下面去了。  
5、如果本机code文件夹下有文件删除了，而远程主机上的play下面该文件没删除，这时候直接同步的话，它不会自动删除远程仓库的文件，需要显示增加- -delete参数才行：  
rsync -r - -delete code/ 192.168.166.141:/home/vhwz/play

#### 简化ssh交互步骤
每次和远程服务器进行交互都要输密码，非常麻烦，以下为解决方案：  
1. 下载ssh-copy-id命令：  
`sudo curl https://raw.githubusercontent.com/beautifulcode/ssh-copy-id-for-OSX/master/ssh-copy-id.sh -o /usr/local/bin/ssh-copy-id`  
2. 为该命令增加执行权限：  
`sudo chmod +x /usr/local/bin/ssh-copy-id`  
3. 在本地生成ssh公钥密码：  
`ssh-keygen`  
这样你在本地的.ssh目录下就能看到新生成的id_rsa和id_rsa.pub两个文件  
4. 将生成的id_rsa.pub这个公钥上传到你的远程服务器上：  
`ssh-copy-id whz@192.168.166.141`  
从此之后，你和该远程主机进行ssh交互就再也不用输入密码了，棒棒哒！  

## 域名解析：
通过电脑访问域名地址的时候，会先到自己电脑的/etc/  hosts目录下查找是否有该域名对应的ip，如果有的话，就不会再去向DNS服务器询问了。  
如果没有，这时候才会去向DNS服务器询问。  
例如：  
在/etc/hosts文件中添加，211.154.172.172 gitpro.com  
当我们访问gitpro.com这个域名的时候，电脑就会知道我们访问的是211.154.172.172这个ip地址。

## 目录树和磁盘的关系：
windows是每个磁盘都有一颗自己的目录树。  
linux中的目录树只有一颗，但可以有多个磁盘。这些磁盘是挂载在linux的目录树上的。  
例如：  
sda1挂载在目录树的根目录节点上，sda2挂载在目录树的home目录节点上。  
我们往home目录下存放的东西，其实质都存放在sda2这个磁盘上的。  
除了home目录之外的地方存放东西，则实质存放在sda1这个磁盘上。

## Vim
#### 基础配置
按照 https://github.com/gmarik/Vundle.vim 的提示进行安装配置。

#### 个性化
基础配置完成后，在.vimrc文件末尾加上以下配置：  
```
syntax on      表示语法高亮打开  
set number     表示显示行号  
set tabstop=4    表示一个tab的空格数，默认是8  
set softtabstop=4   按退格键的时候退回缩进的长度  
set shiftwidth=4   每一级缩进的长度  
set expandtab   缩进用空格表示
```

#### Vundle插件管理
`~/.vim`  是vim真正保存的地方  
`~/.vimrc` 所有关于vim的配置文件都写在这里面  

进入vim，然后输入以下命令，便可以管理插件了。  
`:PluginInstall` 安装插件  
`:PluginInstall!` 更新插件  
`:PluginClean` 清除不在.vimrc文件中的插件  
`:PluginList` 显示已经安装的插件  

#### 基础操作
`vi`  进入vim程序  
`vi code/foo`  打开code/foo这个文件  
`:q`  退出vim程序  
`:q!`  退出vim程序，且无需保存文件。  

`normal mode  `  
进入vi程序时的默认mode  
`command mode  `  
输入 : / 之类的符号，进入command mode。  
`insert mode  `  
输入 i a o 之类的符号，进入insert mode。  

在insert mode下才能输入字符。  
输入完成之后，输入 ： 进入command mode模式  
`:w`  保存文件  
`:wq`  保存文件并退出  

#### 光标移动
在normal mode下移动光标  
![光标移动](https://github.com/bitw404/blog/blob/master/imgs/vim01.png)
同一行之间的移动：  
`0  shift+^  shift+$   w   b  `  
不同行之间的移动：  
`数字+shift+G   shift+G   数字+上下箭头  `  
不同页之间的移动：  
`ctrl+f   ctrl+b  `  
返回页面顶部：  
`gg  `  

#### 编辑操作
在normal mode下  
`a  `  
在一行文本的末尾，输入 a 表示在该行末尾添加文本，自动进入insert mode。  

`o  O  `  
在当前行之下创建一个新的空白行，并进入insert mode  
在当前行之上创建一个新的空白行，并进入insert mode  

`x  dw  dd  d0  `  
`x`表示删除当前字符  
`dw`表示剪切当前word    
`dd`表示剪切当前行  
`d0`表示剪切光标及其光标前的，当前行的所有字符。  

`yw   yy   y0  `  
`y`表示复制  
`p   P  `  
`p`表示粘贴    

`u`  
表示放弃最近一次的修改  

`/  `  
输入 / 进入command mode  
输入字符，进行查找匹配，找到后输入 n 可以在匹配对象之间来回切换。  

#### 多文件操作
`vi foo test.py kk.js  `  
用vim同时打开多个文件  

`:e test.js  `  
如果已经打开了vim，这时候想要再多打开一个文件，可以使用 :e test.js 的方法。  

`:buffers  `  
显示当前vim打开了的所有文件  

`:buffer 3  `  
将当前vim文件切换到第3个  

`:r foo.txt  `  
读取foo.txt文件的内容到当前操作文件的光标位置处。  

`:w foo3  `  
将当前正在操作的文件内容写入foo3这个文件，如果磁盘里没有foo3这个文件则自动新建一个。  