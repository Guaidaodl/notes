# Powershell 下 Git 的 Log 中文显示乱码
在系统环境变量中添加变量LESSCHARSET为utf-8.

# Powershell 下 Git 的 status 不能显示中文.
设置一下 quotepath 的值即可.
``` bash
git config --global core.quotepath false
```

# Powershell 个人配置文件夹的位置
My Documents\WindowsPowerShell\profile.ps1

# 如何安装 fzf
choco install fzf

# 相关文档
- Git 命令相关的请参考 [Git-Cheat-Sheet](Git-Cheat-Sheet.md)