# Git学习笔记

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

#### 场景模拟
```git
提交了不安全的信息到远程仓库，想要删除git的commit历史记录：
git log
找到要回退的历史，输入q退出。
git reset 4caac0f83ac672981a1621ad1860b470a39c9075
git add .
git commit -m 'update'
git push -f
分析：
-f表示强制提交，如果本地和远程仓库有冲突，强制提交后，远程仓库就变成和本地仓库一样了。
如果想要远程仓库、本地仓库的修改同时保留，可使用：git pull
git reset -mixed 只保留源码，回退index和commit，git reset不带参数默认就是这种。
git reset -soft  只回复commit，保留index，想要重新提交直接commit即可。
git reset -hard  彻底回退，连源码都不保留。
```


