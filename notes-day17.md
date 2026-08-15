# Day 17：团队规范模拟

日期：2026-08-14

## 核心概念

规范不是命令，是**沟通协议**——让历史可读、可追溯。

## 1. 分支命名规范

常用前缀约定：
```
feature/<功能名>     功能开发
bugfix/<修复内容>    修 bug
hotfix/<内容>        紧急线上修复
release/<版本>       发布分支
docs/<内容>          文档
chore/<内容>         杂务
```

核心原则：**只看分支名就知道在干什么**。
（审查自己仓库：feature/learning-branch ✓、bugfix/finished01 ✓、cherry ✗、merge ✗）

## 2. 提交信息规范（Conventional Commits）

```
<type>(<scope>): <subject>

type: feat(新功能) fix(修bug) docs(文档) chore(杂务)
      refactor(重构不改行为) style(格式) test(测试) revert(撤销)
```

核心原则：**只看标题就知道改了什么**。
首行 ≤50 字符，动词开头（add/fix/update）。

## 3. 团队协作规矩

1. 每任务开一个分支，别在主分支直接开发
2. 提交信息规范 + 首行精简
3. 完成开发 push -u，走 PR/MR 让同事 review
4. 每天上班先 `git pull` 同步
5. push 前先 `git status` 确认

## 今日练习记录

- 规范流程：feature/add-user-profile 分支 + `feat: add user profile module` + `fix: add email validation`
- 故意造垃圾提交 `dsfadsfasdf` 对比，体会"碍眼 vs 清晰"
- 用 `git reset --soft HEAD~2` 撤销 2 个不规范的 main 提交，重做为规范提交 `docs: add example doc for commit convention`
- 推送成功

## 踩坑/结论

- 垃圾提交信息在 git log 里完全无法回溯（改了什么/为什么），规范提交一望即知
- `reset --soft` 撤销提交、改动留在暂存区，可重做提交（Day 8 实战复用）
- 审查自己历史时先问两个问题：分支名看清用途了吗？提交信息看清改了什么吗？