# Day 25：tag 版本标签

日期：2026-08-16

## 核心概念

- **tag 是"固定不动的指针"**：一旦打上永远指向那个提交，不随新提交移动（对比分支会移动）
- 用途：版本发布标记（v1.0.0）、重要里程碑、随时回到某版本
- 两种类型：
  - **轻量标签**：只是指针，无额外信息
  - **附注标签**（推荐）：带打标签者、日期、说明，有独立哈希（`git tag -a`）

## 关键命令

```bash
git tag -a v1.0.0 -m "说明"   # 打附注标签（推荐）
git tag v1.0.0-beta           # 打轻量标签
git tag                       # 列出标签
git tag -n                    # 列出标签+说明
git show <tag> --no-patch     # 看标签详情
git checkout <tag>            # 检出标签（进入 detached HEAD）
git push origin <tag>         # 推送单个标签（tag 默认不随 push 推送）
git tag -d <tag>              # 删除本地标签
git push origin --delete <tag># 删除远程标签
git ls-remote --tags origin   # 查看远程标签
```

## 今日练习记录

- 打附注标签 v1.0.0（含说明）和轻量标签 v1.0.0-beta，对比两者信息
- 推送 tag：`git push origin v1.0.0`，远程出现 refs/tags/v1.0.0
- 删除演示：本地删 beta，`git push origin --delete v1.0.0` 删远程
- checkout 到 tag：进入 detached HEAD 状态，回到 main 恢复正常

## 踩坑/结论

- **tag 不随 `git push` 推送**，要单独 `git push origin <tag>`（或 `--tags` 全推）
- 同名 tag 已存在会报错：先删旧 tag 或用新版本号
- checkout 到 tag 会进入 detached HEAD，做完要 `git switch` 回分支
- 语义化版本习惯：v主版本.次版本.修订版（v1.0.0、v1.1.0、v2.0.0）
- 团队发布流程：稳定后打 tag → push tag → 记录发布说明