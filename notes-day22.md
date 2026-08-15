# Day 22：git bisect（二分定位 bug）

日期：2026-08-15

## 核心概念

- bisect 用**二分查找**定位"引入 bug 的第一个提交"：告诉它好/坏两个端点，它反复切到中间版本，每次问你判断，约 `log2(N)` 次锁定目标
- 适用场景：知道某个旧版本没问题、当前有问题，但不确定中间哪个提交引入的
- 原理：每次判断排除一半候选，16 个提交约 4 次锁定

## 关键命令

```bash
git bisect start              # 开始二分
git bisect bad [<hash>]       # 标记"坏"（默认当前 HEAD）
git bisect good <hash>        # 标记"好"（已知没 bug 的版本）
# 每次自动 checkout 中间版本，判断后：
git bisect bad / git bisect good   # 反复直到锁定
git bisect reset               # 结束，回到原分支
git bisect log                 # 查看 bisect 过程记录
git bisect run <测试命令>      # 自动化：脚本判断（0=好 非0=坏）
```

## 今日练习记录

- 造 8 个提交的 number.txt 历史，第 4 个（954f3f2）把值改成 -4 模拟 bug
- 完整跑 bisect：bad HEAD → good 最早的 bc1c3ce → 自动切到 commit 4（坏）→ commit 3（好）
- 锁定：`954f3f2 is the first bad commit`（commit 4），仅 2 次判断
- `git bisect reset` 回到原分支，工作区干净
- **练习待补**：用户表示暂时没完全掌握，稍后再练

## 踩坑/结论

- bisect 会**切换工作区**，开始前确保工作区干净（未提交改动会被覆盖）
- 用完必须 `git bisect reset` 回到原分支
- 真实场景配合自动化：`git bisect run <命令>` 让脚本判断
- 锁定后用 `git show <hash>` 看引入 bug 的提交改了什么
- 效率是 `log2(N)`：每次判断排除一半候选