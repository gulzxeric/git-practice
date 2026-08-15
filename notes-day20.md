# Day 20：第 3 周复盘（远程协作）

日期：2026-08-14

## 本周知识地图

| Day | 主题 | 一句话记住 |
|-----|------|-----------|
| 14 | fetch/pull | pull = fetch + merge；fetch 只下载更新 origin/* 指针 |
| 15 | remote 管理 | remote 是昵称→URL 映射；ls-remote 联网验证 |
| 16 | upstream | 追踪关系存 config；-u 建立后裸 push/pull 可用 |
| 17 | 团队规范 | 分支前缀 + Conventional Commits + 协作规矩 |
| 18 | 双端冲突 | push 被拒是保护；pull→解决→push，绝不裸 force |
| 19 | force push | 只用于自己独占分支；永远用 --force-with-lease |

## 本周测验答案

1. fetch 只下载远程提交更新 origin/main，本地不动；pull = fetch + merge（多一步合并，可能冲突）
2. 解法：`git pull` → 解决冲突 → `git push`。**不能**用 force（会覆盖同事提交）
3. `-u` 建立本地分支与远程分支的追踪；没有它裸 push 报 `has no upstream branch`
4. `--force` 无条件覆盖（危险）；`--force-with-lease` 先检查远程是否被他人改过，变了拒绝（stale info）
5. `git remote add origin <url>` → `git remote -v` 看配置 → `git ls-remote origin` 联网验证

## 仓库大整理记录

- 删除 4 个练习分支（feature/add-user-profile、cherry、merge、bugfix/finished01）：`git branch -D`
- 删除远程残留分支（cherry、merge、test、feature/force-demo）：`git push origin --delete`
- `git fetch --prune` 清理过期远程跟踪记录
- 保留 feature/learning-branch（第 1 周纪念）
- 最终：本地 main + feature/learning-branch，远程仅 origin/main

## 第 3 周核心收获

- **从"单机玩家"变"团队玩家"**：理解了本地/远程是独立仓库靠同步联系
- push 被拒 → pull → 解决 → push 的肌肉记忆已建立
- force push 的安全边界（--force-with-lease + 独占分支）已建立
- 密钥安全铁律：上传过 = 泄露，立即 rotate

## 第 4 周预告（进阶收尾）

log 高级查询 → bisect → blame → amend/rebase -i → tag → 工作流 → 全流程演练 → 速查表