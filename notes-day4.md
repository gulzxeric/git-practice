# Day 4：stash（暂存）

日期：2026-08-12

## 核心概念

`stash` 是工作区的"储物柜"：把未提交的改动暂时存起来，让工作区变干净，就能自由切换分支；干完活再取回。

- 比喻：工作区 = 桌面，stash = 抽屉（先进后出）
- stash 存的是**整个工作区的改动**，跟分支无关，任何分支都能 pop 取回
- 适用场景：feature 干到一半，临时要切回 main 修 bug

## 关键命令

```bash
git stash            # 存起未提交改动，工作区变干净
git stash pop        # 取出最近一堆并放回工作区，自动移除记录
git stash list       # 看抽屉里有几堆（stash@{0} 是最新的）
git stash drop       # 扔掉某一堆（不要了）
```

## 今日练习记录

- 演示：改 wip.md 不提交 → `git stash` → 工作区干净 → 可以自由切换 → `git stash pop` 取回
- stash pop 后记录自动删除（`Dropped refs/stash@{0}`）

## 踩坑/结论

- stash 存的是工作区整体改动，不是某分支专属，所以跨分支 pop 也会出现改动
- pop 时若工作区当前状态和 stash 时冲突，同样会弹冲突需要解决
- 抽屉可以堆多堆，后进的编号小（stash@{0} 最新）