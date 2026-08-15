# Day 15：remote 管理与多远程

日期：2026-08-14

## 核心概念

- remote 是**远程仓库的昵称**（昵称 → URL 的映射），`origin` 只是默认约定名，可随意取名
- 远程信息存在 `.git/config` 里：`remote.<名>.url`、`remote.<名>.fetch`、`branch.<分支>.remote`
- 可以配置**多个远程**（如 GitHub + Gitee），push 时用 `git push <远程名> <分支>`
- 本地分支通过追踪关系（upstream）绑定某个远程分支

## 关键命令

```bash
git remote -v                     # 查看所有远程及 URL
git remote add <名> <url>         # 添加远程
git remote set-url <名> <url>     # 修改远程地址（换用户名/ssh）
git remote get-url <名>           # 查看某远程地址
git remote rename <旧名> <新名>   # 重命名远程
git remote remove <名>            # 删除远程
git push <远程名> <分支>          # 推送到指定远程
git config --get-regexp branch  # 查看含 branch 的配置（内置过滤，跨平台通用）
git ls-remote <名>                # 联网验证远程真实存在、能连上（返回分支和哈希）
```

## 今日练习记录

- 演示多远程：`git remote add backup` → `git remote -v` 看到 origin + backup
- 演示 set-url 改地址（example.com → 改回）和 get-url 查看
- 演示 rename（backup→archive）和 remove（删掉 archive），回到单 origin 状态

## 踩坑/结论

- `origin` 只是约定俗成的默认名，不是 Git 强制
- 多远程时 push 必须写远程名，否则推默认的 origin
- `remote remove` 只删本地配置，不影响远程仓库本身
- 换远程地址用 `set-url` 不用删了重加（保留追踪关系）
- **`git remote add` 不联网验证 URL**，假网址/不存在地址也能 add 成功，真正的问题发生在 fetch/push 时（连不上或被权限拒绝，本地代码安全）
- **验证远程用 `git ls-remote <名>`**：真的联网查询，返回远程分支+哈希即成功；报 `Could not resolve host` / 认证失败即连不上
- 自检口诀：`remote -v` 看"我配了啥"（只查本地配置），`ls-remote` 看"真能连上吗"（联网验证）
