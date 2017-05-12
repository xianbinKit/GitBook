# git Avoid debug prinf, 如何避免将prinf合并

来看一个在开发中经常会遇到的情况：我正在解决某个特别棘手的 Bug，为了便于调试而在代码中添加了一些调试命令并向控制台打印了一些信息。

这些调试和打印语句都在它们各自的提交记录里。最后我终于找到了造成这个 Bug 的根本原因，解决掉以后觉得沾沾自喜！

最后就差把`bugFix`分支里的工作合并回`master`分支了。你可以选择通过 fast-forward 快速合并到`master`分支上，但这样的话`master`分支就会包含我这些调试语句了。你肯定不想这样，应该还有更好的方式……

![](/assets/img_debug_printf.png)   -----&gt; action --&gt;  ![](/assets/img_debug_print2.png)      

 我们在master分支上发现了bug, 创建一个debug分支来测试，在debug分支上创建了一个printf分支来打印错误信息和log. 再在printf分支上创建bugFix分支来得到最终解决bug的版本。

##### Cherry-pick 方法

```
git checkout master; git cherry-pick C4;
```

在这里debug分支和C1分支一样，是没有修改的（或者打开了debug开关）， 然后在此基础上添加了printf修改来打印信息，commit之后再创建bufFix分支来进行调整。 最终debug节点上记录了打开debug开关的修改，printf节点上记录了printf命令的修改，而真正bugFix的修改只在C4节点里。所以我们只需要提取C4的节点就好了。



Rebase -i 方法

```
git rebase -i master；（选择C4）; git checkout master;git rebase bugFix;
```

![](/assets/img_debug_print4.png)



 这里可以看到两种方法的区别。显然cherry-pick更清晰。。。

