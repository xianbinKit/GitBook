# Git rebase 重写合并

##### 重写合并

```
git rebase master
```

将当前`branch`合并到`master` 里。

![](/assets/img_rebase.png)       ----&gt;  git rebase master ---&gt;  ![](/assets/img_rebase_2.png)

可以看到创建了`c3'`,  并且提交记录更加清晰了。 但是`master`并没有跟进，还在`c2`.

##### 将master 与 bugFix 统一

```
git checkout master; git rebase bugFix
```

将 `master` 移动只 `bugFix` 分支当前节点。

![](/assets/img_rebase_3.png)

##### 



