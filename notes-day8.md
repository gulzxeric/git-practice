# Day 8：reset 三模式

日期：2026-08-13

## 核心概念

Git 三个区域（reset 的基础）：
```
工作区（Working Tree）  ← 眼睛看到的文件
暂存区（Staging/Index） ← git add 后待打包
提交（Commit/HEAD）     ← git commit 后归档的历史
```

`git reset` 把 HEAD（分支指针）往回调，回退到哪个区域由模式决定：

| 模式 | HEAD | 暂存区 | 工作区 | 用途 |
|------|------|--------|--------|------|
| `--soft` | 回退 | 保留 | 保留 | 撤销 commit，改动留在暂存区 |
| `--mixed`（默认） | 回退 | **清空** | 保留 | 撤销 commit + add，改动回到工作区 |
| `--hard` | 回退 | 清空 | **覆盖抹掉** | 全部回退，未提交改动消失（危险） |

记忆：soft 软到连暂存都留着 → mixed 半吊子（默认）→ hard 彻底抹平。

## 关键命令

```bash
git reset               # 默认 mixed：撤销 add（暂存→工作区），不丢内容
git reset --soft HEAD~1 # 撤销最近1次提交，改动保留在暂存区
git reset --mixed HEAD~1# 撤销提交+暂存，改动回到工作区
git reset --hard HEAD~1 # 撤销提交并抹掉工作区改动（危险，先留后路）
git diff --cached --stat  # 看暂存区有哪些改动
```

## 今日练习记录

- 用 `git reset`（mixed）把"已暂存"变回"未暂存"：`M ` → ` M`，内容保留
- 用 `git reset --soft HEAD~1` 撤销提交：HEAD 回退，改动仍留在暂存区（状态 MM）
- 用 `git reset --hard HEAD~1`：实验提交和未提交改动一起消失，工作区回到目标提交状态

## 踩坑/结论

- **`--hard` 会抹掉未提交的工作区改动**，用之前先 `git stash` 或确认内容
- mixed 是最常用默认值，日常"撤销 add"就裸用 `git reset`
- 丢失的提交不是真没救——明天 Day 9 reflog 能捞（这就是敢用 hard 的底气）
- reset 会移动分支指针，等于改写该分支历史，已推送的提交慎用（团队协作中优先 revert，后补）
