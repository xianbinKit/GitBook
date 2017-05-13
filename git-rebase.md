# Git rebase 重写合并

##### 重写合并

```
git rebase master
```

将当前`branch`合并到`master` 里。

![](/assets/img_rebase.png)       ----&gt;  git rebase master ---&gt;  ![](/assets/img_rebase_2.png)

可以看到创建了`c3'`,  并且提交记录更加清晰了。 但是`master`并没有跟进，还在`c2`.

```
git rebase branch1 branch2
```

 将branch1 合并到branch2上。

##### 将master 与 bugFix 统一

```
git checkout master; git rebase bugFix
```

将 `master` 移动只 `bugFix` 分支当前节点。

![](/assets/img_rebase_3.png)

##### 有选择性的合并

```
git rebase -i <target node>
```

这个命令讲当前节点合并到目标节点， 会弹出UI窗口，让你选择要合并的节点和改变顺序。

