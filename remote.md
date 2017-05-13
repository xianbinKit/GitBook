# Git remote

##### Clone

```
git clone
```

在本地创建一个当前节点的远程分支，这个分支的命令规则为 &lt;remote name&gt;/ &lt; branch name&gt; ， 比如 origin/master

在本地checkout到远程分支之后，commit会进入HEAD分离状态，是因为远程分支并没有进行了实际的改变，因为内容在远程，git 并不允许在本地对远程branch进行修改，本地的远程分支只是更新了git 修改的提交。

```
git checkout origin/master; git commit
```

![](/assets/img_remote.png)

** 本地的远程分支反应了本地远程分支与远程仓库最后一次通信的状态.**

##### Fetch

```
git fetch
```

git fetch 命令将于远程仓库通信，更新所有本地远程branch的状态并下载所需要的文件，但是并不会修改master. 也就是说，只更新了origin/master, 但是没有更新master. 请记住，我们无法在本地对远程分支origin/master操作。

既然我们已经知道了如何用`git fetch`获取远程的数据, 现在我们学习如何将这些变化更新到我们的工作当中。

其实有很多方法的 —— 当远程分支中有新的提交时，你可以像合并本地分支那样来合并远程分支。也就是说就是你可以执行以下命令:

* `git cherry-pick o/master`
* `git rebase o/master`
* `git merge o/master`
* 等等

##### Pull

通常使用fetch更新了origin/master分支后，我们都会希望合并远程的修改和本地的修改。所以会使用merge命令。看这个例子。

![](/assets/img_remote2.png)   -----&gt;  ![](/assets/img_remote3.png)

本地master分支做了C2修改，远程仓库你的同事做了C3修改，并且提交到了远程仓库。当我们使用：

```
git fetch; git merge origin/master;
```

将会把远程修改C3加到本地的远程分支origin/master上，再使用merge命令把本地master分支合并到本地的远程origin/master分支，得到了节点C4,一个基于C2和C3的节点。

由于这个操作非常常用，所以git把它们合并成为了一个操作

```
git pull
```

##### 

##### 

##### Push

```
git push
```

git push是把本地master的修改更新到本地的origin/master\(或者说将origin/master合并到master\), 然后推送到远程仓库。和pull一样，是一系列的操作。



假设你周一克隆了一个仓库，然后开始研发某个新功能。到周五时，你新功能开发测试完毕，可以发布了。但是 —— 天啊！你的同事这周写了一堆代码，还改了许多你的功能中使用的 API，这些变动会导致你新开发的功能变得不可用。但是他们已经将那些提交推送到远程仓库了，因此你的工作就变成了基于项目**旧版**的代码，与远程仓库最新的代码不匹配了。

这种情况下,`git push`就不知道该如何操作了。如果你执行`git push`，Git 应该让远程仓库回到星期一那天的状态吗？还是直接在新代码的基础上添加你的代码，异或由于你的提交已经过时而直接忽略你的提交？

因为这情况（历史偏离）有许多的不确定性，Git 是不会允许你`push`变更的。实际上它会强制你先合并远程最新的代码，然后才能分享你的工作。

![](/assets/img_remote4.png)

 如上例子，假设星期一时，远程仓库版本和你的本地版本都为C1, 当周五时，你做了C3修改，你的同事做了C2修改，并且已经推送到了远程仓库，这时候你尝试push,是不成功的，因为本地并没有C2的修改，而远程仓库上有C2的修改，git并不知道是要把C3加到C1上还是C2上。





