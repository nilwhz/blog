# Git学习笔记

#### 如何建立多个git账户用于ssh登录
```bash
举栗子：已经有github账号，公司使用gitlab账号，如何生成新的ssh key。

1、在生成ssh key的时候，名字要设置不能直接回车（默认是id_rsa，这样就和github的一样了）。
添加私钥：
ssh-add ~/.ssh/id_rsa_github

2、在.ssh目录下输入命令：touch config  创建config文件用于配置ssh登录。
# gitlab 汇游科技
Host hykj
    HostName 114.215.142.80
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_rsa_hykj

# github
Host bitw
    HostName github.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_rsa

3、配置git用户和邮箱
git config --global --unset user.name
git config --global --unset user.email

git config --global user.name "biw404"
git config --global user.email "biw404@gmail.com"

新建一个用于工作的工作目录，例如hykj目录。
mkdir hykj
cd hykj
git init
git config user.name "wanghz"
git config user.email "wanghz@huiyoukeji.net"

4. 添加私钥到本地。
ssh-add -l   显示增加过的私钥
ssh-add -K /Users/vwhz/.ssh/id_rsa_hykj   将私钥增加到本地
ssh-add -l   增加过后再次查看
```

#### GitHub相关命令：
```git
language:Python stars:>10000
搜索stars数量超过10000的所有Python项目
```

#### Git命令:
```git
git ls-files
列出当前追踪的文件

git rm -r —cached cha1_chat/app
删除已经追踪的文件

git remote -v
列出远程仓库地址

git remote set-url origin git@github.com:bitmonk404/test.git
将远程仓库从https转换为ssh协议
```

#### 撤销操作
```git
0、撤销工作区中的修改。配合git status查看：
git checkout -- test.py

1、撤销index暂存区中的操作。配合git status查看：
git reset HEAD test.py

2、撤销commit过后在仓库中的内容。配合git log(输入q退出)查看：
git reset 4caac0f83ac672981a1621ad1860b470a39c9075
git reset --mixed 只保留源码，回退index和commit，git reset不带参数默认就是这种。
git reset --soft  只回复commit，保留index，想要重新提交直接commit即可。
git reset --hard  彻底回退，连源码都不保留。
备注：本地仓库的内容修改后，使用git push -f可以强制更新远程仓库的内容、提交历史。

3、刚提交后就想修改的简单操作：
git commit -m 'update'
git commit --amend
它让你有机会重新写提交信息文字。

git commit -m 'update'
git add kk.py
git commit -amend
它只产生了一次提交，只是增加上了kk.py文件。
```


