# Git checkout : HEAD    跳转当前节点到指定位置

##### 跳转

```
git checkout <branch name or node hashcode>
```

![](/assets/img_checkoutHEAD.png)  ---&gt;  `git checkout C4` ---&gt; ![](/assets/img_checkoutHEAD2.png)

HEAD 表示当前正在什么节点，当指向一个 `branch`时，会有\*表示， 这时候是 `HEAD->bugFix->C4`. 因为`bugFix`分支如果有没有提交的内容，则`bugFix` 分支和C4并不完全一致。

##### 相对跳转

上面的移动命令中，C4 只是一个假设hashcode, 实际的hascode有40位那么长，我们可以通过 git log 来查看hashcode的值。也可以只输入前几位hashcode来实现跳转，只要这个hashcode唯一。

```
git log
```

当然还有更简便的相对移动。

```
git checkout bugFix^
```

如左图所示，我们在bugFix分支， 这条命令表示 从bufFix节点跳到上一个节点，即跳到了C4， 如右图。如果我们想继续往前跳转，可以使用：

```
git checkout HEAD^
```

##### 多步跳转 ~

```
git checkout bugFix~2
```

多次输入^是很烦的，可以直接输入负号+数字来实现直接跳转到某个地方。

#####  连续跳转

 ^富豪后面跟数字表示向上移动一次，但是如果有多个父节点，^表示移动到哪一个父节点，父节点的顺序是根据提交顺序来决定的。



![](/assets/img_checkout5.png)

```
git checkout HEAD~^2~2
```

![](/assets/img_checkout6.png)

