# Day 18：模拟真实远程冲突（双端推送）

日期：2026-08-14

## 核心概念

双端推送冲突：你和同事各自从同一提交出发，各自提交各自 push。后 push 的一方会被拒绝（non-fast-forward），因为远程已经有别人先推的提交，自己的提交接不上去。

```
你的本地:  A ── B ── C(你的新提交)
远程:      A ── B ── D(同事先推了)   ← C 接不上 B，push 被拒
```

**关键**：push 被拒是**保护机制**，防止覆盖别人的提交。解法是 pull → 解决 → push。

## 关键命令

```bash
git push          # 可能报 Updates were rejected (non-fast-forward)
git pull origin main   # 被拒后先拉取并合并远程（可能冲突）
# 解决冲突 → git add → git merge --continue → git push
```

## 今日练习记录

- 用临时目录克隆出"同事工作区"，同事改 merge.txt push（457c24e..91415a4）
- 本地也改 merge.txt push → **被拒**：Updates were rejected
- `git pull` → 冲突（两边都改 merge.txt 同行）→ 解决 → merge --continue → push 成功
- 最终图：cb34f13 合并提交，两条线汇合
- 同事工作区再推 f3ec54d + 73aa512（day2-todo 改动 + 合并）

## 踩坑/结论

- **push 被拒绝对不是错误**，是保护机制
- 遇到 Updates were rejected **绝不能直接 force push**（会覆盖同事提交），必须先 pull
- pull 会 fetch 远程新提交并合并，改同行才冲突，改不同行自动合（Day 3 冲突判定复习）
- 冲突解决套路与 merge 完全一致：读标记 → 编辑 → add → merge --continue
- 排错思路：先看 `git log --oneline --graph --all` 确认分叉，再决定 pull 策略