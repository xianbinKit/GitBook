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

## Push

```
git push
```

git push是把本地master的修改更新到本地的origin/master\(或者说将origin/master合并到master\), 然后推送到远程仓库。和pull一样，是一系列的操作。

```
git push <remote> <place>   // ex: git push origin master
```

如果使用这条命令，git会忽略你当前所在分支，而是直接检测远程仓库origin里master分支和本地master分支的不同，并进行push.

```
git push <remote> <source>:<destination>
```

将不同的分支推送到远程仓库。例如：

```
git push origin foo^:master
```

![](/assets/img_push.png)  --&gt; ![](/assets/img_push2.png)

 如果destination不存在，git会帮创建一个新分支。



假设你周一克隆了一个仓库，然后开始研发某个新功能。到周五时，你新功能开发测试完毕，可以发布了。但是 —— 天啊！你的同事这周写了一堆代码，还改了许多你的功能中使用的 API，这些变动会导致你新开发的功能变得不可用。但是他们已经将那些提交推送到远程仓库了，因此你的工作就变成了基于项目**旧版**的代码，与远程仓库最新的代码不匹配了。

这种情况下,`git push`就不知道该如何操作了。如果你执行`git push`，Git 应该让远程仓库回到星期一那天的状态吗？还是直接在新代码的基础上添加你的代码，异或由于你的提交已经过时而直接忽略你的提交？

因为这情况（历史偏离）有许多的不确定性，Git 是不会允许你`push`变更的。实际上它会强制你先合并远程最新的代码，然后才能分享你的工作。

![](/assets/img_remote4.png)

如上例子，假设星期一时，远程仓库版本和你的本地版本都为C1, 当周五时，你做了C3修改，你的同事做了C2修改，并且已经推送到了远程仓库，这时候你尝试push,是不成功的，因为本地并没有C2的修改，而远程仓库上有C2的修改，git并不知道是要把C3加到C1上还是C2上。

解决这个问题的办法就是先合并远程的修改。

##### 假设我们用rebase来做。

```
git fetch; git rebase origin/master; git push;
```

和merge一样，rebase也有一条简单的命令

```
git pull --rebase; git push;
```

![](/assets/img_remote5.png)

##### 假设我们用merge 来做 \(注意fetch + merge = pull\)

```
git fetch; git merge origin/master; git push
```

![](/assets/img_remoate6.png)

在开发社区里，有许多关于 merge 与 rebase 的讨论。以下是关于 rebase 的优缺点：

优点:

* Rebase 使你的提交树变得很干净, 所有的提交都在一条线上

缺点:

* Rebase 修改了提交树的历史

比如, 提交 C1 可以被 rebase 到 C3 之后。这看起来 C1 中的工作是在 C3 之后进行的，但实际上是在 C3 之前。

一些开发人员喜欢保留提交历史，因此更偏爱 merge。而其他人（比如我自己）可能更喜欢干净的提交树，于是偏爱 rebase。仁者见仁，智者见智。 :D

首先来看`git push`。在远程跟踪课程中，你已经学到了 Git 是通过当前检出分支的属性来确定远程仓库以及要 push 的目的地的。这是未指定参数时的行为，我们可以为 push 指定参数，语法是：

`git push <remote><place>`

`<place>`参数是什么意思呢？我们稍后会深入其中的细节, 先看看例子, 这个命令是:

`git push origin master`

把这个命令翻译过来就是：

_切到本地仓库中的“master”分支，获取所有的提交，再到远程仓库“origin”中找到“master”分支，将远程仓库中没有的提交记录都添加上去，搞定之后告诉我。_

我们通过“place”参数来告诉 Git 提交记录来自于 master, 要推送到远程仓库中的 master。它实际就是要同步的两个仓库的位置。

需要注意的是，因为我们通过指定参数告诉了 Git 所有它需要的信息, 所以它就忽略了我们所检出的分支的属性！

要同时为源和目的地指定`<place>`的话，只需要用冒号`:`将二者连起来就可以了：

`git push origin <source>:<destination>`

这个参数实际的值是个 refspec，“refspec” 是一个自造的词，意思是 Git 能识别的位置（比如分支`foo`或者`HEAD~1`）

一旦你指定了独立的来源和目的地，就可以组织出言简意赅的远程操作命令了，让我们看看演示！

## 指定本地远程分支的名字

直接了当地讲，`master`和`o/master`的关联关系就是由分支的“remote tracking”属性决定的。`master`被设定为跟踪`o/master`—— 这意味着为`master`分支指定了推送的目的地以及拉取后合并的目标。

你可能想知道`master`分支上这个属性是怎么被设定的，你并没有用任何命令指定过这个属性呀！好吧, 当你克隆仓库的时候, Git 就自动帮你把这个属性设置好了。

当你克隆时, Git 会为远程仓库中的每个分支在本地仓库中创建一个远程分支（比如`o/master`）。然后再创建一个跟踪远程仓库中活动分支的本地分支，默认情况下这个本地分支会被命名为`master`。

克隆完成后，你会得到一个本地分支（如果没有这个本地分支的话，你的目录就是“空白”的），但是可以查看远程仓库中所有的分支（如果你好奇心很强的话）。这样做对于本地仓库和远程仓库来说，都是最佳选择。

这也解释了为什么会在克隆的时候会看到下面的输出：

```
local branch "master" set to track remote branch "o/master"
```

当然可以啦！你可以让任意分支跟踪`o/master`, 然后该分支会像`master`分支一样得到隐含的 push 目的地以及 merge 的目标。 这意味着你可以在分支`totallyNotMaster`上执行`git push`，将工作推送到远程仓库的`master`分支上。

有两种方法设置这个属性，第一种就是通过远程分支检出一个新的分支，执行:

`git checkout -b totallyNotMaster o/master`

就可以创建一个名为`totallyNotMaster`的分支，它跟踪远程分支`o/master`。

### 第二种方法

另一种设置远程追踪分支的方法就是使用：`git branch -u`命令，执行：

`git branch -u o/master foo`

这样`foo`就会跟踪`o/master`了。如果当前就在 foo 分支上, 还可以省略 foo：

`git branch -u o/master`

