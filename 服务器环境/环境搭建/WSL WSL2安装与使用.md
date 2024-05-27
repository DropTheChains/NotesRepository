
- 电脑版本：Windows 10
- 虚拟机版本：Ubuntu 24.04


## 在Win 10 安装WSL2

### 第一步：启动WSL

管理员身份启动PowerShell

```powershell

dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart

```

### 第二步：启用虚拟化平台

```powershell

dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart

```

此时重启电脑。

### 第三步：设置WSL2为默认值

```powershell

wsl --set-default-version 2

```

### 第四步：安装Ubuntu

```PowerShell

wsl --list --online

请使用“wsl --install -d <分发>”安装。

NAME                                   FRIENDLY NAME
Debian                                 Debian GNU/Linux
kali-linux                             Kali Linux Rolling
Ubuntu-18.04                           Ubuntu 18.04 LTS
Ubuntu-22.04                           Ubuntu 22.04 LTS
Ubuntu-24.04                           Ubuntu 24.04 LTS
OracleLinux_8_7                        Oracle Linux 8.7
OracleLinux_9_1                        Oracle Linux 9.1
openSUSE-Leap-15.5                     openSUSE Leap 15.5
SUSE-Linux-Enterprise-Server-15-SP4    SUSE Linux Enterprise Server 15 SP4
SUSE-Linux-Enterprise-15-SP5           SUSE Linux Enterprise 15 SP5
openSUSE-Tumbleweed                    openSUSE Tumbleweed
PS C:\Users\chains> wsl --install -d Ubuntu-24.04
正在安装: Ubuntu 24.04 LTS
已安装 Ubuntu 24.04 LTS。
正在启动 Ubuntu 24.04 LTS…



```


安装完成后开始菜单中会出现Ubuntu的图标，如果出现以下报错

```
WslRegisterDistribution failed with error: 0x800701bc

```

需要点击链接安装内核更新包：

https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi

安装完成后再次启动就OK了。



### WSL2迁移Ubuntu


```PowerShell

Windows PowerShell
版权所有 (C) Microsoft Corporation。保留所有权利。

尝试新的跨平台 PowerShell https://aka.ms/pscore6

首先在D盘目录下创建WSL目录和Ubuntu24.04目录 
使用  wsl -l -v  命令查看Ubuntu是否正在运行，显示为Stop状态即可执行

PS C:\Users\chains> wsl --export Ubuntu-24.04 D:\WSL\Ubuntu24.04\Ubuntu.tar
PS C:\Users\chains> wsl --unregister Ubuntu-24.04
正在注销...
PS C:\Users\chains> wsl -l -v
适用于 Linux 的 Windows 子系统没有已安装的分发版。
可以通过访问 Microsoft Store 来安装分发版:
https://aka.ms/wslstore
PS C:\Users\chains> wsl --import Ubuntu-24.04 D:\WSL\Ubuntu24.04   D:\WSL\Ubuntu24.04\Ubuntu.tar --version 2
PS C:\Users\chains> wsl -l -v
  NAME            STATE           VERSION
* Ubuntu-24.04    Running         2
PS C:\Users\chains>


```

迁移之后重启电脑，再次在终端中进入wsl

```
PS C:\Users\chains> wsl
适用于 Linux 的 Windows 子系统现已在 Microsoft Store 中可用!
你可以通过运行“wsl.exe --update”或通过访问 https://aka.ms/wslstorepage 进行升级
从 Microsoft Store 安装 WSL 将可以更快地获取最新的 WSL 更新。
有关详细信息，请访问 https://aka.ms/wslstoreinfo

Welcome to Ubuntu 24.04 LTS (GNU/Linux 5.10.16.3-microsoft-standard-WSL2 x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Sun May  5 20:20:16 CST 2024

  System load:  0.0                Processes:             9
  Usage of /:   0.5% of 250.98GB   Users logged in:       0
  Memory usage: 1%                 IPv4 address for eth0: 172.22.158.110
  Swap usage:   0%

```