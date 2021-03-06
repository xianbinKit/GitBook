# git commit skill: 提交技巧

## Skill 1

接下来这种情况也是很常见的：你之前在`newImage`分支上进行了一次提交，然后又基于它创建了`caption`分支，然后又提交了一次。

此时你想对的某个以前的提交记录进行一些小小的调整。比如设计师想修改一下`newImage`中图片的分辨率，尽管那个提交记录并不是最新的了。

我们可以通过下面的方法来克服困难：

* 先用
  `git rebase -i`
  将提交重新排序，然后把我们想要修改的提交记录挪到最前
* 然后用
  `commit --amend`
  来进行一些小修改
* 接着再用
  `git rebase -i`
  来将他们调回原来的顺序
* 最后我们把 master 移到修改的最前端（用你自己喜欢的方法），就大功告成啦！

当然完成这个任务的方法不止上面提到的一种（我知道你在看 cherry-pick 啦），之后我们会多点关注这些技巧啦，但现在暂时只专注上面这种方法。 最后有必要说明一下目标状态中的那几个`'`—— 我们把这个提交移动了两次，每移动一次会产生一个`'`；而 C2 上多出来的那个是我们在使用了 amend 参数提交时产生的，所以最终结果就是这样了。

##### 重新提交 `git commit --amend`

不管这个节点的父节点是谁（因为我们可以改变顺序）， 当使用amend提交时，会取节点原来提交时的父节点，创建一个新分支来替代原来的分支。

这个问题也可以不还顺序，然后直接跳到newImage上修改，然后在回到caption上进行cherry-pick.并且显然cherry-pick方法更简单。

![](/assets/img_commitskill1.png)--&gt;  action --&gt; ![](/assets/img_commitskill2.png)



```
git checkout newImage
git commit --amend
git checkout master
git cherry-pick newImage caption
```

---

---



