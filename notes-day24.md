# Day 24：amend 与提交整理（rebase -i）

日期：2026-08-16

## 核心概念

- **amend**：替换"最近一次提交"，不是追加。会改写提交哈希（重写历史）
- **rebase -i**（interactive）：整理任意多个提交——合并(squash)、改信息(reword)、重排、删除(drop)
- 两者都改写历史，只适用于**未推送**的提交；已推送的需配合 force push

## 关键命令

```bash
git commit --amend -m "新信息"    # 修改最近提交的提交信息
git commit --amend --no-edit      # 补充漏掉的文件（信息不变）
git commit --amend                # 打开编辑器改信息
git rebase -i HEAD~3              # 交互式整理最近 3 个提交

# rebase -i 编辑器的操作（每行 pick 可换成）：
#   pick   保留
#   reword 保留但改提交信息
#   squash 并入上一个提交
#   edit   保留但暂停（用于拆分）
#   drop   删除
```

## 今日练习记录

- amend 补漏：提交 app.js 后漏了 style.css → `git commit --amend --no-edit` 补进同一提交
- amend 改信息：`git commit --amend -m`，哈希从 31ed331 变 e0841cc
- rebase -i 造 3 个叠加提交（part1/2/3）→ 后两个改 squash → 合并成 1 个提交 07cd9cc
- 用 GIT_EDITOR 指向脚本实现非交互 squash

## 踩坑/结论

- **amend 会改哈希**，未推送才安全；已推送要用 force
- rebase -i 非交互执行的技巧：GIT_EDITOR 指向"修改 todo 的脚本"（脚本接收文件路径参数，读+改+写）
- 之前演示踩坑：新建文件做 rebase 会触发 add/add 冲突（base 没有该文件）；**叠加修改已有文件**则顺畅
- rebase 卡住时：`git rebase --abort` 放弃 / `git rebase --continue` 继续 / `git rebase --quit` 结束会话
- squash 后提交信息会合并显示，可再 amend 规范化
- 有 rebase 残留状态时（error: cannot lock ref），先 `git rebase --quit` 清理再操作