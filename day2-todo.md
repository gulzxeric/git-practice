11
22
33
44

1. 在 main 上建 feature/day2-merge：git switch -c feature/day2-merge
2. 切回 main，创建 todo.md（3 行内容 A），提交
3. 切到 feature/day2-merge，创建 todo.md（3 行内容 B），提交
4. 切回 main，git merge feature/day2-merge
5. 观察是否出现 Merge made by the 'ort' strategy 和新的合并提交
>>>>>>> feature/day2-merge
