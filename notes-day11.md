# Day 11：restore 与 checkout 的选择

日期：2026-08-13

## 核心概念

- `git restore` 是**只针对单个文件/暂存区**的精细恢复手术刀，不动任何指针（对比 reset 是移动整个 HEAD）
- 三个方向：
  - 工作区 → `git restore <file>`（放弃工作区改动）
  - 暂存区 → `git restore --staged <file>`（撤销 git add，内容保留）
  - 任意提交 → `git restore --source=<commit> <file>`（从旧提交恢复）
- **checkout 老命令被拆分**：Git 2.23+ 把 `git checkout` 拆成 `switch`（切分支）+ `restore`（恢复文件）。现在 checkout 只负责切分支

## 关键命令

```bash
git restore <file>               # 放弃工作区改动（永久丢，谨慎）
git restore --staged <file>      # 撤销 git add，回到未暂存（内容保留）
git restore --source=<hash> <file>  # 从任意提交恢复文件内容
# 老写法（已淘汰）：
git checkout -- <file>           # 等价 git restore <file>
```

## 今日练习记录

- 演示放弃工作区改动：改坏 wip.md → `git restore wip.md` 恢复干净
- 演示撤销 add：改 + add → `git restore --staged` → `M ` 变 ` M`，内容保留
- 演示从旧提交恢复：`git restore --source=HEAD~1 wip.md` 替换为旧版本
- 清理现场后工作区干净

## 踩坑/结论

- `git restore <file>` 是**永久丢弃**未提交改动（没进过提交的改动 reflog 救不了），用前想清楚
- `--staged` 不丢内容，只是把文件从暂存区退出来
- 决策速查：reset=整个历史（本地）、revert=已推送提交、restore=单个文件/暂存区
- 老命令 checkout 身兼两职已被拆分，新代码里优先用 switch/restore

## 第 2 周撤销全家桶速查

| 需求 | 命令 |
|------|------|
| 撤销整个提交历史（本地） | `git reset --soft/mixed/hard` |
| 撤销已推送提交 | `git revert` |
| 放弃某文件工作区改动 | `git restore <file>` |
| 撤销某文件的 add | `git restore --staged <file>` |
| 从旧提交恢复文件 | `git restore --source=<hash> <file>` |
| 找回"丢失"的提交 | `git reflog` → `git reset --hard "HEAD@{N}"` |
