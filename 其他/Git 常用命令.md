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
## Branch 相关
- 列出当前的 branch
  ```
  git rev-parse --abbrev-ref HEAD
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
  
## Powershell 与 fzf
  ```Powershell
  function Switch-Git-Branch 
  {
      $br = Select-Git-Branch
      Write-Output $br
      if (-not [String]::IsNullOrEmpty($br)) {
          git checkout $br.trim()
      }
  }

  function Select-Git-Branch
  {
      if (($args.Count -eq 1) -and ($args[0] -eq '-r')) {
          $bs = git branch -r
      } else {
          $bs = git branch
      }
      if ([String]::IsNullOrEmpty($bs)) { return }

      return (Write-Output $bs | fzf.exe)
  }
  ```
 
 

