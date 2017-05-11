# Git merge 合并分支

#####  合并

```
git merge bugFix
```

将`bugFix`分支合并到当前分支。此时，`c4`有两个父节点，这个节点包含了两条分支的修改。

![](/assets/img_merge.png)



#####  将所有分支统一

 假如我们用 `git checkout bugFix; git merge master` 命令 将`c4` 合并到`c2`, 那么`master`分支和`bugFix`分支都会合并到`c4`节点，且每条分支的修改都一样了。

![](/assets/img_merge_2.png)

