# Day 12：cherry-pick（挑单提交）

日期：2026-08-14

## 核心概念

- merge/rebase 搬**整条分支**；cherry-pick 精准搬**单个提交**
- 典型场景：
  - main 上有 hotfix，feature 分支也想用 → 只 pick 这一个提交
  - 误提交到错误分支 → pick 到正确分支后删掉原分支的
  - 不想 merge 整条线（会带上无关改动）
- **cherry-pick 是重新生成提交**：内容一样，但哈希会变（因为父提交不同）

## 关键命令

```bash
git cherry-pick <hash>        # 把指定提交搬到当前分支
git cherry-pick --continue    # 解决冲突后继续
git cherry-pick --abort       # 放弃本次 cherry-pick
```

## 今日练习记录

- main 上造修复提交 c9ff0b5 → 在 merge 分支 cherry-pick 它 → 生成新提交 0e54e0c
- 验证：内容一致（bugfix.txt 两边都有），哈希不同（重新生成）
- git diff main merge 确认 merge 分支自己的改动（cc.txt、merge.txt）未被带入

## 踩坑/结论

- cherry-pick 后的提交哈希必然不同，属正常现象
- pick 的改动和当前分支冲突时，同 merge 一样弹冲突：解决 → `git add` → `git cherry-pick --continue`
- 放弃用 `git cherry-pick --abort`
- 与 merge/rebase 的区别：后者搬整条分支，前者只搬一颗提交