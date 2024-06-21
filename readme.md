# Git

## `git pull` & `git pull --rebase`

在dev分支上执行操作

```
git pull
git push

# 等价于
git fetch
git merge origin/dev
git push
```

```
git pull --rebase
git push

# 等价于
git fetch
git rebase --origin/dev
git push
```

## `git reset`

[`git reset`三种模式](https://www.jianshu.com/p/c2ec5f06cf1a)

1. `git reset --hard` (暂存区和工作区的东西都会舍弃)
2. `git reset --soft` (暂存区和工作区保持不变，reset导致的差异转到暂存区)
3. `git reset --mixed` (default) (暂存区、工作区、reset导致的差异通通转到工作区.效果看起来就是原节点和Reset节点之间的所有差异都会放到工作目录中)

## `git revert`

[`git revert`使用以及理解](https://blog.csdn.net/allanGold/article/details/111372750)

## `git diff`

- `git diff`: 当工作区有改动，临时区为空，diff的对比是“工作区与最后一次commit提交的仓库的共同文件”；当工作区有改动，临时区不为空，diff对比的是“工作区与暂存区的共同文件”
- `git diff --staged` 或 `git diff --cached`: 显示暂存区(已add但未commit文件)和最后一次commit(HEAD)之间的所有不相同文件的增删改(`git diff --cached`和`git diff –staged`相同作用)
- `git diff HEAD`: 显示工作目录(已track但未add文件)和暂存区(已add但未commit文件)与最后一次commit之间的的所有不相同文件的增删改
  - `git diff HEAD~X` 或 `git diff HEAD^^^…`(后面有X个^符号，X为正整数):可以查看最近一次提交的版本与往过去时间线前数X个的版本之间的所有同上一条中定义文件之间的增删改
- `git diff <branch1> <branch2>`: 比较两个分支上最后 commit 的内容的差别
  - `git diff branch1 branch2 --stat`    显示出所有有差异的文件(不详细,没有对比内容)
  - `git diff branch1 branch2`              显示出所有有差异的文件的详细差异(更详细)
  - `git diff branch1 branch2 具体文件路径` 显示指定文件的详细差异(对比内容)

## `git cherry-pick`

[`git cherry-pick`使用以及理解](https://www.ruanyifeng.com/blog/2020/04/git-cherry-pick.html)

## indetermination

main分支 / dev分支

```
git checkout -b dev_xx
# 在dev_xx分支上
git commit
git fetch origin dev
git merge dev  # 需要的话解决冲突

# 在dev分支上
git merge dev_xx
git push
```

## todo

- [`git fetch`](https://www.yiibai.com/git/git_fetch.html)
- [Git删除远程某个历史提交记录](https://www.jianshu.com/p/18b5cbc3e702)
- [`git rebase`](https://lvan-zhang.blog.csdn.net/article/details/128848133?spm=1001.2101.3001.6650.2&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-2-128848133-blog-106479779.235%5Ev43%5Epc_blog_bottom_relevance_base9&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-2-128848133-blog-106479779.235%5Ev43%5Epc_blog_bottom_relevance_base9&utm_relevant_index=1)