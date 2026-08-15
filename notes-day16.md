# Day 16：upstream 与追踪关系

日期：2026-08-14

## 核心概念

- **upstream（上游）** = 本地分支跟踪的那个远程分支，存在 config 里两行：
  - `branch.<分支>.remote = origin`（远程名）
  - `branch.<分支>.merge = refs/heads/main`（远程具体分支）
- 建立追踪后，裸 `git push` / `git pull` 不用写参数，Git 自动知道推/拉哪
- 无追踪的分支裸 push 会报错：`fatal: The current branch <名> has no upstream branch.`
- `git branch -vv` 显示 `[origin/x: ahead N, behind M]`：ahead = 本地领先提交数，behind = 落后数

## 关键命令

```bash
git push -u origin <分支>          # 推送 + 建立追踪（-u = --set-upstream）
git push --set-upstream origin <分支>  # 同上（完整写法）
git branch --set-upstream-to=origin/<分支> <本地>  # 修改追踪目标
git branch -vv                     # 查看追踪关系 + ahead/behind
git config --get-regexp branch     # 查看分支相关配置（跨平台，不依赖 grep）
```

## 今日练习记录

- 裸 push main（有追踪）：正常，`Everything up-to-date`
- cherry 分支（无追踪）裸 push：报 `has no upstream branch`，提示修复方法
- `git push -u origin cherry`：建立追踪成功，GitHub 提示可建 PR
- `git branch --set-upstream-to=origin/main cherry`：换绑，显示 `ahead 3, behind 11`
- 改回 origin/cherry 追踪

## 踩坑/结论

- 追踪关系 = 本地分支绑定远程分支，存在 config 里
- 有追踪 → 裸 push/pull 自动工作；无追踪 → 报错
- `--set-upstream-to` 改绑后 `branch -vv` 立刻显示新的 ahead/behind
- `git config --get-regexp <关键词>` 是内置过滤，跨平台通用（比 `list | grep` 强）
- push -u 成功后远程会提示创建 PR 的链接（为 PR 流程埋伏笔）