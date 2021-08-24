```
出错: 不能启动多个虚拟服务

1. 关闭hyper-v，用命令：以管理员启动 powershell，执行：
bcdedit /set hypervisorlaunchtype off
2. 关闭wsl虚拟机（重点） 以管理员启动 powershell，执行：
Disable-WindowsOptionalFeature -Online -FeatureName VirtualMachinePlatform
```