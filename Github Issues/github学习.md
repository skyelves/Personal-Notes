### 拉取指定branch代码

```shell
git clone -b <branchName> https://xxx.git
```

拉去所有submodule

```shell
git clone --recurse-submodules https://xxx.git
```

更新submodule

```shell
git submodule update --init --recursive
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



### 取消git add

已经git commit，只取消commit，不取消add

```shell
git reset --soft HEAD^
```

--mixed 

意思是：不删除工作空间改动代码，撤销commit，并且撤销git add . 操作

这个为默认参数, git reset --mixed HEAD^ 和 git reset HEAD^ 效果是一样的。

--soft  

不删除工作空间改动代码，撤销commit，不撤销git add . 

--hard

删除工作空间改动代码，撤销commit，撤销git add . 

注意完成这个操作后，就恢复到了上一次的commit状态。

 

 如果commit注释写错了，只是想改一下注释，只需要：

git commit --amend

此时会进入默认vim编辑器，修改注释完毕后保存就好了



HEAD^的意思是上一个版本，也可以写成HEAD~1

如果你进行了2次commit，想都撤回，可以使用HEAD~2



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
git remote add origin HTTPS_URL # to undo: git remote remove origin
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



## Git 删除contributor

https://stackoverflow.com/questions/44563131/removing-contributor-from-github-com/44563345

ViFi's answer works:

Assuming, it is being done with all the right intentions and, you are the owner of repository - you can use `rename` feature on repository. Essentially, create replica of repository and swap repository names like you swap variables with steps below.

1. Create a new `replica` repository
2. Copy the cherry picks from `original` repository which have only the commits with intended authors.
3. Rename the `original` repository to `to_be_deleted` and `replica` to `original`.

Commits from original repository can be picked with following steps.

- `git remote add repo2 https://github.com/mygit/original.git`
- `git pull repo2`
- `git cherry-pick <commit>`
- `git push `

Contributors are essentially the authors of any commit in the repository. I once accidentally put a wrong email in Author list of a commit in my repository and github started showing a new contributor in the repository. I tried [reverting the commit](https://ncona.com/2011/07/how-to-delete-a-commit-in-git-local-and-remote/) but it didn't help. Finally I had to create / rename /delete original repository.





## Git 删除文件

```shell
git rm <filename>
git commit -m "rm file"
git push
```



## Git 查看当前账户

```shell
git config user.name
git config user.email
```



## Git 切换账号

```shell
git config --global user.name "John Doe" 
git config --global user.email "john@doe.org"
```

