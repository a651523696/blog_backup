---
title: git revert的陷阱
date: 2019-01-09 16:13:48
tags: [git]
---



假设一开始master分支上有两个commit

![](/images/git-revert-issue/commit1.png)

这时候我们切换到一个新分支develop并做了一个新的commit
这时候仓库历史是这样的<!--more-->
![](/images/git-revert-issue/commit2.png)

此时再切换回master后,执行`git merge develop`

![](/images/git-revert-issue/commit3.png)

但此时如果发现develop还不应该merge到master,因此在master上对上一个commit执行了**revert**, `git revert 9e84a`,这时候的历史就变成了

![](/images/git-revert-issue/commit5.png)

这时如果你想重新把develop merge到master, 回到master,执行`git merge develop`

会发现提示`Already up-to-date.` 这是为什么呢, 因为**revert**本身是重新做了一个commit把**被revert**的commit的内容改回去了,但实际`git log` 显示的被revert的commit还在历史中,比如这里`9e84a`,所以你重新把develop往master上merge的时候,git发现develop上的内容master上都有了.

总结:不能把**revert** 理解为`git reset`