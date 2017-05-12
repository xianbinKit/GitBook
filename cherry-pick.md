# Cherry-pick 修改提交记录

![](/assets/img_cherry_pick.png)

```
git cherry-pick C3 C4 C7
```

 master本来在C1的位置，从C1拉出来三条线分别实现了不同的功能，这时候要将三条线都合并到master,但是又不想将所有的修改记录都通过rebase的方式进行添加，因为不是所有的修改信息都是有效的，这时候可以通过cherry-pick来选择添加内容。

