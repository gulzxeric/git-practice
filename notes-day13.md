# Day 13：第 2 周复习（撤销与后悔药）

日期：2026-08-14

## 本周知识地图

| Day | 主题 | 一句话记住 |
|-----|------|-----------|
| 8 | reset 三模式 | soft=回退留暂存 / mixed=回退清暂存(默认) / hard=回退抹工作区 |
| 9 | reflog | 后悔药：HEAD 每次移动都记账，找回任何"丢失"提交 |
| 10 | revert | 已推送提交的安全撤销：新增反向提交，不改历史 |
| 11 | restore | 单个文件/暂存区的精确手术刀（取代 checkout 文件职责） |
| 12 | cherry-pick | 精准搬单个提交到当前分支（重新生成，哈希变） |

## 决策速查（本周核心）

| 场景 | 命令 |
|------|------|
| 撤销 add（未提交） | `git restore --staged <file>` |
| 放弃工作区改动 | `git restore <file>` |
| 撤销本地提交（改写历史） | `git reset --soft/mixed/hard HEAD~N` |
| 撤销已推送提交 | `git revert <hash>` |
| 找回"删掉的"提交 | `git reflog` → `git reset --hard "HEAD@{N}"` |
| 搬单个提交 | `git cherry-pick <hash>` |
| 从旧提交恢复文件 | `git restore --source=<hash> <file>` |

## 综合测试题

### 场景 A：误 add 了文件
刚 `git add` 了一个不想提交的文件，工作区改动想保留。怎么处理？

### 场景 B：本地提交撤销
昨天本地提交了 2 个垃圾提交，还没推送，想抹掉它们但保留改动。怎么处理？

### 场景 C：已推送的错误提交
3 天前提交了个错误改动用 `git push` 推给了团队，别人已经 pull。怎么撤销？

### 场景 D：删掉的分支
之前 `-D` 删了分支，突然想起上面有个关键提交。怎么找回来？

### 场景 E：跨分支搬修复
main 上有个 hotfix 提交，feature 分支想单独用，不想 merge 整条。怎么做？

## 结论

- 第 2 周核心收获：**从"怕搞坏"变成"敢乱操作"**——reflog 兜底 + 决策速查
- 口诀：改自己的用 reset，改团队的用 revert；单文件用 restore，单提交用 cherry-pick
