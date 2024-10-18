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

## `git tag`

[`git tag`使用以及理解](https://blog.csdn.net/QH_JAVA/article/details/77979622)

```
# 创建带有说明的标签，用-a指定标签名，-m指定说明文字
$ git tag -a v0.1 -m "version 0.1 released push url" d5a65e9

# push所有tag
$ git push origin --tags
```

## 仓库克隆

```
# 通过ssh将git仓库克隆到本地指定路径并重命名
$ git clone git@github.com:username/repo.git /path/to/newname
```

## 一些常用命令
```
# 创建并切换到对应分支
git checkout -b <branch_name>

# 强制将一个分支指针移动到指定的提交或位置
git branch -f <branch_name> <commit>
```

## indetermination

### 开发过程

dev分支

```
git checkout -b feat

# 在feat分支上
git commit

# 在dev分支上
git pull
git merge feat  # 有需要的话解决冲突
git push
```

### 冲突
无论是`git merge`还是`git rebase`执行后遇到冲突, 终端可能会显示一个vim编辑器, 用于解决冲突。可以退出该编辑器, 使用vscode等解决冲突, 冲突解决后, **测试、测试、测试**！一切正常后, 对于merge操作, `git add .`然后`git commit`; 对于rebase操作, `git add .`然后`git rebase --continue`。(没有冲突的文件均已添加到暂存区, 目的是只需要集中处理发生冲突的文件)

## todo

- [`git fetch`](https://www.yiibai.com/git/git_fetch.html)
- [Git删除远程某个历史提交记录](https://www.jianshu.com/p/18b5cbc3e702)
- [`git rebase`](https://lvan-zhang.blog.csdn.net/article/details/128848133?spm=1001.2101.3001.6650.2&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-2-128848133-blog-106479779.235%5Ev43%5Epc_blog_bottom_relevance_base9&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-2-128848133-blog-106479779.235%5Ev43%5Epc_blog_bottom_relevance_base9&utm_relevant_index=1)


(以下内容来自于chatgpt)在 Git 的交互式 rebase（`git rebase -i`）中，您可以使用多种命令来修改提交历史。以下是一些常用命令及其含义：
  1. **pick**: 保留这个提交，作为历史的一部分。
  2. **reword**: 保留这个提交，但修改提交信息。
  3. **edit**: 停在这个提交上，让您可以更改内容或提交信息。
  4. **squash**: 将这个提交合并到前一个提交，并允许您修改合并后的提交信息。
  5. **fixup**: 类似于 squash，但会丢弃这个提交的提交信息，直接合并到前一个提交。
  6. **exec**: 执行 shell 命令，可以用于在 rebase 过程中运行脚本或命令。
  7. **drop**: 删除这个提交，不将其包含在新的历史中。
  8. **label**: 为当前的提交创建一个标签，用于后续的引用。
  9. **reset**: 将 HEAD 重置到指定的标签或提交，常用于更改 rebase 的进度。
  10. **merge**: 将当前提交与之前的提交进行合并，适用于复杂的合并场景。