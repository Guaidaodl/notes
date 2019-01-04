- log 列出每个修改的提交的文件

  ```
  git log --stat
  ```
 
- 生成 Patch 文件
  ```
  git patch-format <commit-id1>..<commit-id2>
  ```

- 显示指定 HashTag 的 Commit
  ```
  git show <hash-tag>
  ```
## 花式 diff
- 两个 branch 之间的 diff 
  ```
  git diff branch1..branch2
  ```
- diff 只显示文件名:
  ```
  git diff --name-only
  ```
- diff 只显示文件的增删改查
  ```
  git diff --stat
  ```
 
 

