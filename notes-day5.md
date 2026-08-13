# Day 5：分支删除与整理

日期：2026-08-13

## 核心概念

- 删除分支 = 删掉一个标签（指针），提交对象仍在 .git 里（没人引用则成为"悬空"提交，可用 reflog 找回）
- `-d`（delete）**安全模式**：检查分支是否已合并进当前分支
  - 已合并 → 放行删除（改动不会丢，因为提交已在 main 里）
  - 未合并 → **拒绝**并提示改用 `-D`
- `-D`（强制）：无视检查，未合并分支也删

## 关键命令

```bash
git branch -d <name>       # 安全删除（有合并检查）
git branch -D <name>       # 强制删除（跳过检查）
git branch --merged        # 列出已合并进当前分支的分支
git branch --no-merged     # 列出未合并的分支
git branch -m <old> <new>  # 重命名分支（-m = move）
```

## 今日练习记录

- 删除 3 个已合并分支（feature/day2-merge、feature/day3-a、feature/eric），全部 `-d` 成功
- 尝试 `git branch -d bugfix/hot` 被拒绝：`the branch 'bugfix/hot' is not fully merged`
- 未合并分支暂时保留，等学会 reflog 后再处理

## 踩坑/结论

- **默认只用 `-d`**，它拒绝时先思考是否真该删（`-D` 要谨慎）
- `-d` 的拒绝是保护：未合并分支删掉标签后，提交虽在 .git 里但"找不到入口"了
- 删除分支不立即清空磁盘，提交对象还在，reflog 可捞
