### 拉取指定branch代码

```shell
git clone -b <branchName> https://xxx.git
```



### 查看所有的分支

```
git branch -a  
```



### 查看远程分支

```
git branch -r  
```



### 切换分支

```
git checkout <branchName>
```



### 创建本地分支

```
git branch <branchName>
```



### 删除本地分支

```
git branch -d <branchName>
```



### 创建远程分支

```
git branch <branchName>
git push origin <branchName>
```



### 删除远程分支

```
git push origin --delete <branchName>
```



### 提交代码

```shell
git status                          # 查看本地代码状态

git add .                           # 添加修改代码到缓存

git commit -am "一些信息"   				   # 提交

git checkout -b [branchName]				# 切换分支

git push origin [branchName]        # push进去了！
```

如果branch已经存在，需要事先git branch -d [branch]一下，再切换分支



### 代码回滚

```shell
git reset -–hard commit_id
```



多人协作的工作模式通常是这样：

1. 首先，可以试图用`git push origin <branch-name>`推送自己的修改；
2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
3. 如果合并有冲突，则解决冲突，并在本地提交；
4. 没有冲突或者解决掉冲突后，再用`git push origin <branch-name>`推送就能成功！
5. 如果`git pull`提示`no tracking information`，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream-to <branch-name> origin/<branch-name>`。



### 合并commit

```undefined
git rebase -i HEAD~2
```

将第二行pick改为s，保存退出

![1](/Users/wangke/Desktop/lab/github学习/1.png)

弹出新的界面修改注释

![2](/Users/wangke/Desktop/lab/github学习/2.png)



```
git push -f origin <branchName>
```



## 不同分支合并代码

将error_count代码合并到dev-v1.3.1分支

rebase之前需要经master分支拉到最新

切换分支到需要rebase的分支，这里是dev分支

执行git rebase master，有冲突就解决冲突，解决后直接git add . 再git rebase --continue即可

```shell
git checkout error_count
git rebase dev-v1.3.1
解决冲突
git add <冲突文件>
git rebase --continue
```

https://www.jianshu.com/p/f7ed3dd0d2d8



##根据本地代码创建github仓库

先手动在github上创建一个仓库

在本地代码目录下

```shell
git init
git add xxx
git commit -m ‘first commit’
git remote add origin HTTPS_URL
git pull origin main --allow-unrelated-histories
git push origin main
```



### Git push报错

报错信息：

```shell
LibreSSL SSL_connect: SSL_ERROR_SYSCALL in connection to github.com:443
```

解决方法：

```shell
vi .git/config
```

把url从https改成ssh

```yaml
[core]
        repositoryformatversion = 0
        filemode = true
        bare = false
        logallrefupdates = true
        ignorecase = true
        precomposeunicode = true
[remote "origin"]
        url = git@github.com:skyelves/nvmkv.git 
        #之前是https://github.com/skyelves/nvmkv.git
        fetch = +refs/heads/*:refs/remotes/origin/*
```

