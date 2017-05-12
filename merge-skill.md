# Merge Skill 合并技巧

当在非常多的分支上进行了开发时，可以使用多次rebase到master,得到有序的修改提交。

![](/assets/img_merge_skill.png)

```
git rebase master bugFix
git rebase bugFix side
git rebase side another
git rebase another master
```

![](/assets/img_merge_skill2.png)

