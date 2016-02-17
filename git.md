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


