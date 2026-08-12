# Git 精通学习计划（Spec）

日期：2026-08-12
状态：已批准

## 目标

通过 4 周、每天 2 小时、边练边学的方式，掌握 Git 的中高级技能，为进入企业团队协作环境做准备，同时满足个人项目管理的需求。

当前基础：已掌握 config、log、add、gitignore、status、pull、push、commit。需要加强分支、撤销、远程协作、工作流。

## 学习方式

- 每天 30-40 分钟概念学习 + 剩余时间在练习仓库 C:\Users\30841\Desktop\git 动手实操
- 所有命令都有 reflog 保险，练坏也能恢复
- 最终产出：一个带完整分支历史、故意制造并解决的冲突、规范提交记录的练习仓库

## 课程大纲

### 第 1 周：分支

| 天 | 主题 | 关键命令 |
|----|------|----------|
| 1 | 分支的本质（HEAD 指针、创建=贴标签） | branch / checkout / switch -c |
| 2 | 合并 merge（fast-forward、3-way、冲突） | merge |
| 3 | 解决冲突（读懂冲突标记） | 手动编辑 + add + commit |
| 4 | stash 与暂存 | stash push/pop/list/drop |
| 5 | 分支删除与整理 | branch -d / -D / 重命名 |
| 6 | rebase 入门（与 merge 对比） | rebase |
| 7 | 复盘：用 log --graph 回看分支图 | log --graph |

### 第 2 周：撤销与后悔药

| 天 | 主题 | 关键命令 |
|----|------|----------|
| 8-9 | reset 三模式（soft/mixed/hard） | reset |
| 10 | reflog（找回丢失的提交） | reflog |
| 11 | revert（用于已推送提交） | revert -m |
| 12 | restore 与 checkout 的选择 | restore --source |
| 13 | cherry-pick（挑单提交） | cherry-pick |
| 14 | 综合救援演练 | — |

### 第 3 周：远程协作（团队导向）

| 天 | 主题 | 关键命令 |
|----|------|----------|
| 15 | fetch vs pull 本质 | fetch / pull |
| 16 | remote 管理与多远程 | remote -v / add / set-url |
| 17 | upstream 与追踪关系 | --set-upstream / -u |
| 18 | 团队规范模拟（命名、Conventional Commits） | — |
| 19 | 模拟真实远程冲突（双端推送） | pull |
| 20 | Force push 时机（--force-with-lease） | push --force-with-lease |
| 21 | 复盘周 3 | — |

### 第 4 周：进阶与收尾

| 天 | 主题 | 关键命令 |
|----|------|----------|
| 22 | log 高级查询 | --author / --grep / -S / -G |
| 23 | git bisect 二分定位 | bisect |
| 24 | blame 历史考古 | blame |
| 25 | amend 与 interactive rebase | amend / rebase -i |
| 26 | tag 版本标签 | tag |
| 27 | 工作流与全流程综合演练 | Git Flow / GitHub Flow |
| 28 | 收尾：整理速查表 + 能力自评 | — |

## 成功标准

1. 能独立完成完整开发流程：需求 → 建分支 → 开发 → 冲突解决 → 合并 → 打标签
2. 能用 reflog 找回任何"丢失"的提交
3. 能区分 reset / revert / restore / checkout 的适用场景
4. 理解 fetch 与 pull 的区别，会配置多个远程
5. 明白团队协作中分支命名与提交信息规范的意义
6. 能用 bisect 二分定位 bug 引入的提交

## 所需准备

- 练习仓库：C:\Users\30841\Desktop\git（当前为空，无提交）
- GitHub 账号：第 3 周需要建空仓库做远程练习
- 速查卡工具（Obsidian/Notion 等），随时记录踩过的坑
