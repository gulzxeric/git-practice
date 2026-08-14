# Day 14：第 3 周远程协作（fetch/pull）

日期：2026-08-14

## 核心概念

- pull = fetch + merge
- fetch：下载远程提交到本地，但不合并，只更新远程跟踪指针
- pull：一步到位，fetch 后直接合并进当前分支

## 关键命令

```bash
git remote add origin <url>   # 添加远程
git remote -v                 # 查看远程
git push -u origin main       # 首次推送并建立追踪
git fetch origin              # 下载远程改动但不合并
git pull                      # fetch + merge 一步到位
git branch -r                 # 查看远程跟踪分支
```

## 今日练习记录

（待补）
这个是github网页上改的
