# Day 26：工作流与全流程演练

日期：2026-08-16

## 核心概念：三种主流工作流

1. **GitHub Flow**（小团队/开源/持续部署，最简单）：只有 main + feature，所有改动走 PR 评审后合并
2. **Git Flow**（大型严谨产品）：main（生产）+ develop（开发）+ feature/release/hotfix 各司其职
3. **Trunk-Based**（快速迭代）：主干频繁提交 + 短命分支（<1天）+ 强 CI

| 场景 | 推荐 |
|------|------|
| 开源/小团队/持续部署 | GitHub Flow |
| 严谨产品/固定发版 | Git Flow |
| 快速迭代/强 CI | Trunk-Based |

## 全流程演练记录（2026-08-16）

完整走通"需求到发布"：
1. 从 main 开 `feature/user-auth` 分支
2. 规范提交（feat: add auth login/register）
3. `rebase -i` squash 两个小提交成一个，`amend` 规范化信息
4. main 上有他人改动（refactor auth）→ `git rebase main` 同步 → add/add 冲突 → 解决 → continue
5. `push -u` 推送功能分支（建立追踪）
6. 模拟评审通过 → `git merge` → **Fast-forward**（rebase 的价值体现）
7. push main → `git tag -a v1.1.0` → `git push origin v1.1.0` 发布
8. 清理：`git branch -d` + `git push origin --delete`

## 踩坑/结论

- rebase -i squash 时**第一个提交不能 squash**（没有上一个），只改后续提交的 pick→squash
- rebase 到最新 main 后合并是 fast-forward，历史干净无合并提交——这就是"整理派"工作流的好处
- 完整流程 = 分支 + 规范提交 + rebase 整理 + 冲突解决 + push + 评审 + 发布 tag + 清理，缺一不可
- 一个人也能完整演练团队流程（用 clone 模拟同事、用 rebase 模拟同步）
- 工作流选择取决于团队规模/发布节奏/CI 能力，没有绝对最优