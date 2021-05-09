## 常用工具知识总结

本部分主要是笔者关于常用工具所做的笔记，如果出现错误，希望大家指出！

### 目录

* [GIT](#git)
    * [1. git 与 svn 的区别在哪里？](#1-git-与-svn-的区别在哪里)
    * [2. 经常使用的 git 命令？](#2-经常使用的-git-命令)
    * [3. git pull 和 git fetch 的区别](#3-git-pull-和-git-fetch-的区别)
    * [4. git rebase 和 git merge 的区别](#4-git-rebase-和-git-merge-的区别)


### GIT

#### 1. git 与 svn 的区别在哪里？
   ```
   git 和 svn 最大的区别在于 git 是分布式的，而 svn 是集中式的。因此我们不能再离线的情况下使用 svn。如果服务器
   出现问题，我们就没有办法使用 svn 来提交我们的代码。

   svn 中的分支是整个版本库的复制的一份完整目录，而 git 的分支是指针指向某次提交，因此 git 的分支创建开销更小
   并且分支上的变化不会影响到其他人。svn 的分支变化会影响到所有的人。

   svn 的指令相对于 git 来说要简单一些，比 git 更容易上手。
   ```
   详细资料可以参考：
   [《常见工作流比较》](https://github.com/geeeeeeeeek/git-recipes/wiki/3.5-%E5%B8%B8%E8%A7%81%E5%B7%A5%E4%BD%9C%E6%B5%81%E6%AF%94%E8%BE%83)
   [《对比 Git 与 SVN，这篇讲的很易懂》](https://juejin.im/post/5bd95bf4f265da392c5307eb)
   [《GIT 与 SVN 世纪大战》](https://blog.csdn.net/github_33304260/article/details/80171456)
   [《Git 学习小记之分支原理》](https://www.jianshu.com/p/e8ad60710017)

#### 2. 经常使用的 git 命令？
* mkdir XX：创建一个空目录 XX指目录名

* pwd：显示当前目录的路径

* cat xx：查看xx文件内容

* <font color=red>git init：把当前的目录变成可以管理的git仓库，生成隐藏的.git文件夹</font>

* <font color=red>git add xx：把xx文件添加到暂存区</font>

* <font color=red>git commit -m “xx”：提交文件 -m后面的是注释，必须写！</font>

* git status：查看仓库状态

* git log：查看历史记录

* git reset --hard HEAD^：往上回退一个版本（版本回退）

* git reset --hard 版本号 回退到指定版本号的版本（版本穿梭）

* git reflog：查看历史记录的版本号id

* git checkout -- xx：把xx文件在工作区的修改全部撤销

* git rm xx：删除xx文件

* <font color=red>git remote add origin https://github.com/xxxxx/a.git 关联一个远程库</font>

* <font color=red>git push -u（第一次尽量加上-u，以后不用）origin master：把当前master分支推送到远程库</font>

* <font color=red>git clone https://github.com/xxxxx   从远程库中克隆</font>

* <font color=red>git checkout -b dev：创建dev分支 并切换到dev分支上</font>

* <font color=red>git branch：查看当前所有的分支</font>

* <font color=red>git checkout master：切换回master分支</font>

* <font color=red>git merge dev：在当前分支合并dev分支</font>

* git branch -d dev：删除dev分支

* <font color=red>git branch xxx：创建分支xxx</font>

* git remote：查看远程库信息

* git remote -v查看远程库的详细信息

* <font color=red>git pull origin master 将远程库的更新拉取到本地并自动合并</font>

* <font color="red">git fetch origin master:tmp  新建一个tmp分支，将远程仓库的master分支上的代码复制到tmp分支上，不会自动合并</font>

* <font color=red>git push origin master：git会把master分支推送到远程库对应的分支上</font>

* **<font color="green">git checkout -b my origin/my  此操作主要是针对clone操作后，本地只会显示master分支，要根据远程my分支创建本地my分支 </font>**

   详细资料可以参考：
   
   [《常用 Git 命令清单》](http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html)


#### 3. git pull 和 git fetch 的区别 
   ```
   git fetch 只是将远程仓库的变化下载下来，并没有和本地分支合并。

   git pull 会将远程仓库的变化下载下来，并和当前分支合并。
   ```
   [《详解 git pull 和 git fetch 的区别》](https://blog.csdn.net/weixin_41975655/article/details/82887273)

#### 4. git rebase 和 git merge 的区别
   ```
   git merge 和 git rebase 都是用于分支合并，关键在 commit 记录的处理上不同。

   git merge 会新建一个新的 commit 对象，然后两个分支以前的 commit 记录都指向这个新 commit 记录。这种方法会
   保留之前每个分支的 commit 历史。

   git rebase 会先找到两个分支的第一个共同的 commit 祖先记录，然后将提取当前分支这之后的所有 commit 记录，然后
   将这个 commit 记录添加到目标分支的最新提交后面。经过这个合并后，两个分支合并后的 commit 记录就变为了线性的记
   录了。
   
   总结：如果你想要一个干净的，没有merge commit的线性历史树，那么你应该选择git rebase
   如果你想保留完整的历史记录，并且想要避免重写commit history的风险，你应该选择使用git merge

   ```
   [《git rebase 和 git merge 的区别》](https://www.jianshu.com/p/f23f72251abc)
   [《git merge 与 git rebase 的区别》](https://blog.csdn.net/liuxiaoheng1992/article/details/79108233)