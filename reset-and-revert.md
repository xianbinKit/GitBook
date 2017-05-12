# Reset and Revert 撤销

##### Reset

```
git reset HEAD~1
```

 完全删除记录并跳到指定节点，只可以用于本地的节点。

##### Revert

```
git revert HEAD~1
```

将指定节点作为新的修改，添加新节点到当前节点。 这个方法不会修改已经有的节点，在远程仓库时，多人协作，如果修改了记录，别人就无法使用了。

![](/assets/img_revert.png)

 可以看到新节点其实是C1的一个拷贝。

