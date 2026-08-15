# Day 21：log 高级查询

日期：2026-08-15

## 核心概念

log 不只是"看历史"，是**查询工具**——过滤器 + 格式器组合，精准回答"谁、何时、改了什么、改了哪个文件"。

## 关键命令

```bash
# 结构过滤
git log --oneline --graph --all   # 图 + 全分支
git log --merges                   # 只看合并提交
git log -- <文件>                  # 看该文件所有提交历史
git log --all -- <文件>            # 全分支上的该文件历史

# 内容过滤
git log -p <文件>                  # 看文件每次改动 diff
git log -S "关键词"                # 内容全文搜索（pickaxe）
git log --grep="词"                # 按提交信息搜
git log --author="名"              # 按作者搜

# 范围控制
git log -N                         # 最近 N 个
git log --since/--until="日期"     # 时间过滤
git log A..B                       # B 有而 A 没有的提交

# 格式控制
git log --stat                     # 每个提交改的文件 + 行数
git show <hash> --stat             # 看某提交改了什么
```

## 今日练习记录

- `--grep="secret"` 按提交信息找到密钥相关提交
- `-S "sk-secret"` 按内容搜索：只找到笔记提交（密钥提交已被 force 覆盖，不在历史）
- `--stat` 看最近提交改了哪些文件
- `--since="7 days ago"` 数出 7 天内 84 次提交
- `--author="Eric"` 过滤自己的提交
- `git log --all -- merge.txt` 回溯 merge.txt 从创建到冲突合并的完整历史

## 踩坑/结论

- **`-S` 搜内容，`--grep` 搜提交信息**——对象不同，别混
- 被 force/改写删除的历史用 log 找不到（但 reflog 里还在）——再次印证 Day 19
- `git log -1 -- <文件>` 找到的如果是合并提交，用 `git show <hash>` 看详情
- 团队考古标准动作：`git log -- <文件>` → `git show <hash>` → 定位谁引入的问题