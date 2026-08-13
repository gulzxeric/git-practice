# Day 9：reflog（后悔药）

日期：2026-08-13

## 核心概念

- Git 从不真正删除：每次移动指针（commit/reset/checkout/merge/rebase/stash）都会把"移动前你站在哪"记进 **reflog（引用日志）**
- 被 `--hard` 抹掉、被 `-D` 删分支的提交，其实还在 .git 里活着，只是没人引用，reflog 是找回入口
- 只要操作在本地仓库，reflog 能找回几乎任何"丢失"的提交
- **保留期**：默认 90 天（`gc.reflogExpire`）
- **仅限本地**：reflog 不会被 push

## 关键命令

```bash
git reflog              # 看 HEAD 移动历史（含已"丢失"提交）
git reflog -N           # 只看最近 N 条
git reset --hard "HEAD@{N}"   # 时光机：回到 reflog 记录的某个位置（恢复"事故"）
git branch <新名> <hash>      # 用哈希重建分支
```

## 今日练习记录

- 查看 reflog，认出 Day 8 被 `--hard` 清掉的实验提交 `78092ce` 仍在记录中
- 制造"事故"：`git reset --hard HEAD~2` 丢掉 2 个提交 → 用 `git reset --hard "HEAD@{1}"` 完整救回
- 教训：`HEAD@{1}` 在 PowerShell 必须加引号，否则 `{}` 被解析成脚本语法报 `unknown switch 'e'`

## 踩坑/结论

- **PowerShell 必踩坑**：`HEAD@{N}` 要写成 `"HEAD@{1}"`，加引号
- 找回通用公式：`git reflog` 找目标 → `git reset --hard "HEAD@{N}"`
- reflog 是本地仓库的，不随 push 共享
- 有了 reflog 做底气，第 2 周开始可以放心用 `--hard` 实验

## 补充：-D 删除分支 vs reflog 的边界

- `git branch -D aa` 删的是 `refs/heads/aa` 引用及其专属 reflog（`git reflog show refs/heads/aa` 报 unknown revision）
- **HEAD 的 reflog 是独立全局账本**：只要你在该分支上 checkout/commit 过，HEAD 就记住了那些提交，`-D` 删不掉
- 找回：`git reflog` 找哈希 → `git branch <新名> <哈希>` 重建分支
- 真丢的唯一场景：HEAD 从未"站"过的提交（正常操作碰不到）
