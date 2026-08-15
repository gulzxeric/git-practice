# Day 19：Force push 的时机

日期：2026-08-14

## 核心概念

- 普通 push 只允许**线性推进**（fast-forward）。改写历史（reset/rebase）后本地与远程分叉，普通 push 被拒
- force push 强制覆盖远程，**可能抹掉别人的提交**——最危险的命令
- `--force-with-lease` 安全版：先检查"远程是否还是我上次 fetch 的样子"，变了就拒绝（stale info）

## 关键命令

```bash
git push --force-with-lease   # 安全强制推送（检查远程是否被他人改过）
git push --force              # 无条件覆盖（危险，别用）
git ls-remote origin <分支>   # 看远程实际状态
git rev-parse origin/<分支>   # 看本地认知的远程状态
```

## 今日练习记录

- 造"已推送密钥提交"场景：推送带密钥提交 → 本地 reset --hard 抹掉 → 重新提交干净版
- 普通 push 被拒：`the tip of your current branch is behind its remote counterpart`（这里不能 pull，会把密钥拉回来）
- `git push --force-with-lease` 成功：`+ f1fbd62...08753e4 (forced update)`，密钥提交从远程抹掉
- 模拟"同事在你 fetch 后又推了提交"：`--force-with-lease` 拒绝 `(stale info)`，保护同事提交

## 踩坑/结论

- **黄金规则**：永远用 `--force-with-lease`，不用裸 `--force`
- force push 只用于**自己的分支**；**共享分支（main）绝不 force push**
- 改写历史后**不能 pull**（会把要抹掉的东西又拉回来），直接 force-with-lease
- 被拒的 `stale info` 是好消息——lease 保护了同事的提交
- 要 force 前先 `git fetch` 让本地认知最新，lease 才能正确判断
- `git branch -D` 删本地分支 + `git branch -r --delete` 删远程跟踪分支

## 密钥泄露与应对（安全铁律）

- **密钥一旦上传过就视为"已泄露"**，删除/force push 是补救但**不可靠**
- 泄露路径：① 自己 clone 仓库看历史 ② 任何 clone 过的人（本地副本还在）③ reflog ④ GitHub 侧缓存/日志（不可控）
- 实测：f1fbd62 提交被 reset + force 覆盖后，`git show f1fbd62:force-demo.md` 仍能读出密钥 sk-secret123
- **正确做法：立即吊销旧密钥、生成新密钥（rotate）**，再考虑清理历史
- 根本防线：密钥不入库（.gitignore + 环境变量），提交前检查

## Force push 使用时机

- **合法**：只在自己独占、无人协作的分支上清理/改写历史
  - 清理个人 PR 分支的乱提交
  - 抹掉已推送的敏感信息
  - 修正自己刚推的提交（amend 后覆盖）
  - rebase 到最新 main 后更新远程
- **禁止**：main/master 共享分支、同事在用的分支、已 merge 的提交
- **决策口诀**：谁能看到这个分支？只有你 → force-with-lease；别人也在用 → 绝对不行