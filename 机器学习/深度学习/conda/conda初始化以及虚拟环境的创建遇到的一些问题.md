## PowerShell 使用conda命令创建并激活虚拟环境所遇到的问题

### 🚨 问题1 conda activate d2l之后提示符不显示（d2l）

这是因为 Conda 没有正确初始化 PowerShell 以显示环境名称。虽然 Conda 环境实际上已经激活，但 PowerShell 的提示符没有更新来显示当前环境名称。  

<mark>解决方案：</mark>需要初始化 Conda 的PowerShell 支持

1. 以管理员身份运行 PowerShell

2. 初始化 Conda 的 PowerShell 支持，在管理员 PowerShell 中运行以下命令：
```bash
 conda init powershell
```
3. 重启 PowerShell
关闭所有 PowerShell 窗口，然后重新打开一个普通的 PowerShell（不需要管理员权限）。

4. 验证修复，现在再次尝试激活环境

### 🚨 问题2 再次打开PS之后报错
在初始化 Conda 后，PowerShell 试图执行你的个人配置文件（profile.ps1），但系统的执行策略（Execution Policy）禁止了脚本运行。  

PowerShell 的执行策略是一项安全功能，旨在控制脚本的运行条件，以防止运行不安全的脚本。默认的策略通常是 **Restricted**（限制），这个策略会禁止任何脚本的执行。  

<mark>解决方案：</mark>修改执行策略  

1. 以管理员身份运行 PowerShell

2. 修改执行策略
```powershell
 Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```
系统提示时输入 Y 确认更改

其中**RemoteSigned** 策略允许运行本地脚本，但要求网络下载的脚本必须有数字签名

3. 验证更改

```powershell
 Get-ExecutionPolicy -Scope CurrentUser
```
应该返回 RemoteSigned

4. 重启 PowerShell

重新打开普通 PowerShell 窗口
