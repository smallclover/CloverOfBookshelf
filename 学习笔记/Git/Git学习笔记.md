# Git学习笔记

## 知识点

> [Git在线教程](https://learngitbranching.js.org/?locale=zh_CN)
>
> 上面的链接提供了教程和在线操作。建议一边实践，一边学习理论。

+ git的提交记录保存的是目录下所有文件的快照
+ git的分支是轻量的，只是简单的指向某个提交记录，因此不会造成存储和内存上的开销，可以理解为创建了一个指向某一个提交记录的指针。
+ 创建一个新的分支，就是基于当前的提交和它的父提交进行新的工作。
+ `git merge <branch-name>` 与当前的分支和并，并将当前分支的指针指向合并后的节点。合并后的节点包含两个分支的所有提交记录。
+ `git rebase <branch-name>` 将当前分支的副本移动到指定分支的下一个节点。使用rebase命令能够得到一个更加线性的提交记录。
+ git合并分支的两种方式是merge和rebase

2020年8月25日 **顺**

+ HEAD，可以看作一个总是指向最近一次提交记录的指针，HEAD也可以指向分支名
+ `git checkout <记录hash>` 来将HEAD指向此hash所代表的提交记录。
+ `git rebase -i HEAD~5` 打开rebase的UI模式。

2020年8月26日 **顺**

+ fast-forward，子分支合并到master分支时，如果master分支没有改变过，就直接把master移动到子分支上，合并完成。
+ 如果有过修改，就会合并修改生成一个新的提交记录，并将master移动到这个新的提交记录。（HEAD也会指向这里，之前提到过，HEAD总是指向最近的一次提交）
+ merge和rebase适应的环境和解决的问题是不一样的，merge会完整的呈现所有提交记录的状态。而rebase会将提交记录合并成一个线性记录。一眼看上去比较直观，也比较清晰。

2020年8月27日 **顺**

