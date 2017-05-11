# Git branch 分支

##### 创建

```
git branch <bugFix>
```

创建一个bugFix的分支。

##### 跳转

```
git checkout <bugFix>
```

跳转到bugFix分支。

##### 创建并跳转

```
git checkout -b <bugFix>
```

这条命令等同于上面两条之和。

![](/assets/img_checkout.png)



##### 将分支强制定义到节点

```
git branch -f master bugFix~2
```

将master分支指定到这个节点。可以看到master分支的历史记录只有C0和C1了。



![](/assets/img_branch_f.png)---&gt;`git branch -f master bugFix~2 `---&gt;![](/assets/img_gitbranch3.png)

