# Day 2：merge（合并）

日期：2026-08-12

## 核心概念

merge 把两个分支的改动合到一起，分三种结果：

1. **fast-forward（快进）**：feature 领先、main 无新改动 → main 指针直接前移，**不产生新提交**
2. **3-way merge（三方合并）**：两边都各自提交 → Git 合并改动，**产生合并提交 M**（有两个父提交）
3. **冲突（conflict）**：两边改了同一行 → Git 停下，等你手动选择

## 关键命令

```bash
git merge <branch>       # 把指定分支合并进当前分支
git log --oneline --graph --all   # 查看分支图
git branch -v            # 查看各分支指向的提交
```

## 今日练习记录

- 在 main 上合并 feature/learning-branch → **Fast-forward** 成功
- 观察：合并后 main 和 feature 指向同一个提交，无新合并提交
- 下一步：制造 3-way merge 场景（两分支各自改同一文件不同内容）

## 踩坑/结论

- fast-forward 不是"复制文件"，只是指针移动
- 只有双方分叉时才会产生合并提交
