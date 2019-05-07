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
- 获取 git 的目录, 可以用来判断是否在 git 目录里
  ```
  git rev-parse --git-dir
  ```
- 列出所有的分支和该分支上的最后一个提交者.
  ```
  git for-each-ref --format='%(committerdate) %09 %(authorname) %09 %(refname)' | sort -k5n -k2M -k3n -k4n
  ```
## Branch 相关
- 列出当前的 branch
  ```
  git rev-parse --abbrev-ref HEAD
  ```
- 列出两个分支的不同
  ```
  git cherry branch
  ```
  -v 除了 hash 值外还附带 commit log 的首行
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
## 密码相关

### 设置密码的保存方式.

可以通过设置 credential.helper 来设置密码的保存方式. 可选值有:
- cache 使用内存缓存. 过一段时间后清空
- store 明文保存到文件中.
- osxkeychain 使用 Mac 系统的密码存储.

### 清空 ssh private key 的密码
运行:
```
ssh-keygen -p
```
 
## Powershell 与 fzf
```Powershell
# 通过 fzf 选择一个分支. -r 选项可以选择远程分支.
function Select-Branch
{
    if (($args.Count -eq 1) -and ($args[0] -eq '-r')) {
        $bs = git branch -r
    } else {
        $bs = git branch
    }
    if ([String]::IsNullOrEmpty($bs)) { return ""}

    $selectedBranch = (Write-Output $bs | fzf.exe)
    if ([String]::IsNullOrEmpty($selectedBranch)) { return ""}

    # 去掉 origin/
    return $selectedBranch.trim() -replace 'origin/'
}

# 切换到 fzf 选择的分支, -r 选项可以选择远程分支.
function Switch-Branch 
{
    $br = Select-Branch
    if (-not [String]::IsNullOrEmpty($br)) {
        git checkout $br
    }
}

function Merge-Branch
{
    $br = Select-Branch
    if (-not [String]::IsNullOrEmpty($br)) {
        git merge $br
    }
}

# 将当前分支提交到 Gerrit 上.
function Push-Gerrit
{
    if (-not (git rev-parse --git-dir)) {
        return
    };

    $branchName = git rev-parse --abbrev-ref HEAD

    git push origin HEAD:refs/for/$branchName
}

Set-Alias -Name gch -Value Switch-Branch
Set-Alias -Name gsb -Value Select-Branch
Set-Alias -Name gpg -Value Push-Gerrit
Set-Alias -Name gmb -Value Merge-Branch
```
 
 

