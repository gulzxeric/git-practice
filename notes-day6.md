# Day 6：rebase 入门

日期：2026-08-13

## 核心概念

merge 和 rebase 解决同一个问题（整合两个分支），但哲学不同：

- **merge（保守派）**：保留分叉，产生合并提交 M，历史真实记录"发生过分叉"
- **rebase（整理派）**：把 feature 的提交连根拔起，重新种到 main 最新点之后，结果是**一条直线**，仿佛从未分叉

| | merge | rebase |
|---|---|---|
| 历史形态 | 有分叉、有合并提交 | 一条直线，干净 |
| 提交是否变化 | 原提交保留 | **提交哈希会变**（重写） |
| 谁的历史变了 | main 增加合并提交 | feature 的提交被重写 |

**核心教训**：rebase 会改写提交（哈希变），**绝不要 rebase 已推送、别人也在用的分支**。

## 关键命令

```bash
git rebase <branch>           # 把当前分支的提交搬到 <branch> 之后
git rebase --continue         # 解决冲突后继续（不是 git commit！）
git rebase --abort            # 放弃本次 rebase，回到开始前
git rebase --skip             # 跳过当前提交（不要它了）
$env:GIT_EDITOR="true"; git rebase --continue  # 跳过编辑器，直接用默认提交信息
```

rebase 冲突解决流程：编辑文件 → `git add <file>` → `git rebase --continue`

## 今日练习记录

- 造分叉：main 和 feature 各改 rebasing.md 同一行 → rebase 触发冲突
- 解决冲突后执行 `git rebase --continue`，卡在 vim 编辑器 → 用 `GIT_EDITOR=true` 跳过解决
- rebase 成功：`7a6914a` 变成 `f7e60e2`（哈希变了 = 提交被重写）
- 切回 main 合并 feature → **Fast-forward**（没有合并提交、没有分叉、直线历史）

## 踩坑/结论

- **rebase 冲突的"继续"命令是 `git rebase --continue`，不是 `git commit`**，两者容易搞混
- `git rebase --continue` 默认会打开编辑器确认提交信息，非交互环境会卡住，用 `GIT_EDITOR=true` 跳过
- rebase 后 feature 变成"基于最新 main"，此时合并是 fast-forward，历史整洁
- **红线**：绝不对已推送/共享的分支 rebase，会重写历史毁掉别人
- 决策建议：本地未推送的个人分支用 rebase 整理；共享分支用 merge 保留历史
