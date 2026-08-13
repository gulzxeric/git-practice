# AGENTS.md

## 项目性质

这是一个 **Git 学习练习仓库**（C:\Users\30841\Desktop\git），用于通过边练边学的方式精通 Git。当前无业务代码，所有提交都是为了练习 Git 命令而故意制造的实验性修改。

## 学习计划

4 周 / 每天 2 小时，详见 `docs/superpowers/specs/2026-08-12-git-mastery-plan-design.md`。

- 第 1 周：分支（merge、冲突解决、stash、rebase）
- 第 2 周：撤销与恢复（reset、reflog、revert、restore、cherry-pick）
- 第 3 周：远程协作（fetch/pull、remote、upstream、force push）
- 第 4 周：进阶（log、bisect、blame、rebase -i、tag、工作流）

## 当前进度

按需更新：当前处于第 1 周。

## 协作约定

- 本仓库是练习场地，**故意制造冲突和"破坏性"操作是学习的一部分**，不要阻止用户实验
- 用户请求"练习 X"时：先解释核心概念（30-40 分钟的量），再给出可执行命令让用户动手，最后复盘
- 所有命令都要提醒用户有 reflog 保险
- 每次练习后，鼓励用户做小结笔记（建议 Obsidian/Notion，不放入本仓库）
- **每天学习内容同步写入 `notes-dayN.md` 到本仓库**（用户明确要求），commit 后更新该文件
- 笔记结构：核心概念、关键命令、今日练习记录、踩坑/结论
- **铁律：每天课程开始时先创建当天 `notes-dayN.md` 骨架；课程内容讲完立即直接补全完整笔记并 commit，不要等用户提醒、不要只留骨架**

## 命令约定

- 用户学习新命令时，先演示 1 个安全示例，再让用户自行尝试
- 涉及已推送提交的破坏性操作，默认先推荐安全方案（revert > reset hard + force）
- 提交练习结果时使用 Conventional Commits 风格（如 `feat:`, `docs:`, `chore:`）
