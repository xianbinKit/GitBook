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

##### Push

```
git push
```

 git push是把本地master的修改更新到本地的origin/master\(或者说将origin/master合并到master\), 然后推送到远程仓库。和pull一样，是一系列的操作。

































