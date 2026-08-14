# Day 14：第 3 周远程协作（fetch/pull）

日期：2026-08-14

## 核心概念

- 本地仓库和远程是两个独立仓库，靠同步联系（push 上行 / fetch-pull 下行）
- **pull = fetch + merge**（一步到位）
- fetch：下载远程提交到本地，只更新远程跟踪指针（origin/main），本地分支和工作区**不动**
- pull：fetch 后直接合并进当前分支，**可能冲突**

## 关键命令

```bash
git remote add origin <url>   # 添加远程
git remote -v                 # 查看远程
git push -u origin main       # 首次推送并建立追踪（-u = --set-upstream）
git fetch origin              # 下载远程改动但不合并
git pull origin main          # fetch + merge 一步到位
git branch -r                 # 查看远程跟踪分支
git branch -vv                # 查看本地分支的追踪关系
git diff main origin/main     # fetch 后对比本地与远程差异
git log main..origin/main     # 看远程独有的提交
```

## 今日练习记录

- 配置远程 origin → 首次 push -u 建立追踪 → 验证 origin/main 出现
- GitHub 网页模拟远程他人改动 → **fetch**：本地 main 不动，origin/main 前进（偷看不采纳）
- 造分叉：本地提交 87c2c41 + 远程 4fc1dda 各自改 notes-day14.md → **pull 触发冲突**
- 解决冲突（保留远程内容）→ merge --continue → push 回远程
- 验证本地/远程同步到 b3ef0c2

## 踩坑/结论

- **fetch 后要趁早看差异**：一旦 pull 合并，`git diff main origin/main` 和 `git log main..origin/main` 就空了（两边已同步）
- pull = fetch + merge，所以 pull **可能冲突**，解决套路与 merge 完全一致
- 冲突标记中 HEAD = 本地当前版本，`>>>>>>>` 后是远程分支（如 4fc1dda）
- pull 前最好先 fetch 看差异，避免意外
- 首次 push 用 `-u` 建立追踪，之后裸 `git push` / `git pull` 即可
