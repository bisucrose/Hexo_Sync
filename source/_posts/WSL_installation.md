---
title: Windows Subsystem for Linux安装教程与使用方法（GUI与终端安装）
date: 2024-11-13 10:12:08
tags: [教程,WSL]
top: true
---

# WSL2安装教程与使用方法（GUI与终端安装）

## 前言

<span style="color:red">**注意，本教程会过时！！！**</span>**请永远以官方文档 [安装 WSL | Microsoft Learn](https://learn.microsoft.com/zh-cn/windows/wsl/install) 为准。**~~如果你要当时间警察当我没说。~~

昨天与琉璃一起安装的时候盲目按照自己2021年初的方法配置，~~自己硬造出来了一大堆bug，~~现在看了官方文档以后发现很多地方都不一样了，特别是当年WSL1刚刚出的时候，配置极其繁琐与麻烦，现在的配置步骤相较于以前已经精简了许多。

这里推荐一下Windows应用商店里面全新构建的终端[Windows Terminal|微软应用商店 ](https://apps.microsoft.com/detail/9n0dx20hk701?launch=true&mode=full&hl=zh-cn&gl=cn&ocid=bingwebsearch)，长得颜值还可以，字体也比较好看，各种颜色都比较丰富，可以一试。~~（本人极其颜控，软件长得丑会极大地衰减学习兴趣）~~

## 导航

> Windows 11 & Windows 10 2004（内部版本19041）及以上用户请查看：[GUI版安装教程](#GUI版安装教程（强烈推荐）)
>
> Windows 10 LTSC 2021 用户请查看：[终端自动安装教程](#终端自动安装 )；或者在启用微软应用商店后查看[GUI版安装教程](#GUI版安装教程（强烈推荐）)
>
> Windows LTSC和Server和版本号低于2004的用户请查看[手动安装教程](#手动安装教程)



## GUI版安装教程（小白强烈推荐）

### 常规安装步骤

1. 首先请确保你的Windows版本大于Windows10 2004（内部版本号19041）。

   查看方法：按下Win+R，输入`winver`，弹出的对话框中即可显示当前的系统版本。

2. 直接在Microsoft Store中搜索Ubuntu 24.04 LTS或者你想要的版本（Debian，ArchLinux等）如下图，点击安装。

   ![image-20241113112142656](WSL_installation/image-20241113112142656.png)

2. 微软应用商店会帮你处理所有事情，理论上来讲经历两次重启以后（第一次在点下安装的1分钟左右，第二次在安装完成之前），就可以用了。

3. 按下Win+S，输入`Powershell`或`cmd`或者你自己安装的终端。输入

   ```shell
   wsl -l -v
   ```

   应当显示如下内容：

   ![image-20241113112011487](WSL_installation/image-20241113112011487.png)

5. 安装完毕

### 问题汇总：

> 1. 目前大部分WSL应用均要求WSL2，如果你在应用商店安装过后发现上述步骤三中的截图中Version显示为1，则应当使用以下命令将WSL版本切换为2
>
>    ```shell
>    wsl --set-version Ubuntu-24.04 2
>    ```
>
>    请将上文中的 `Ubuntu-24.04` 更改为自己想切换的发行版
>
>    想知道WSL1和WSL2的区别以及什么时候需要使用WSL1，请参考官方文档：[比较 WSL 版本 | Microsoft Learn](https://learn.microsoft.com/zh-cn/windows/wsl/compare-versions?source=recommendations)
>
> 2. 如果你想安装的版本应用商店里面没有，或者是你没有微软应用商店，请参考下文终端自动安装方式。
>
> 3. 在微软应用商店安装Ubuntu 20.04 LTS时，可能在执行 `wsl --update` 的时候报错，内容如下：
>
>    ![img](WSL_installation/2c0b83b5a2cae8ed3e3d7b50a7180510.png)
>
>    再次执行 `wsl --install` 和其他的所有wsl操作时，会出现以下界面，报错1603，并永远卡死在这里：
>
>    ![img](WSL_installation/fe8ca171e6ff08b4e1d987b1ced4b011.png)
>
>    经查询全网都没有解决方法，也没有人提出相关问题。自己以前倒是遇到过此类情况，原因为安装软件时软件错误地配置了注册表键值权限，导致它自己没有足够的权限，无法配置。我在电脑上重新安装了WSL2，发现这些键值会重新出现，因此个人认为直接删除这几个目录即可。<span style="color:red">**注意：如有疑虑请自行考虑解决方法。**</span>
>
>    以管理员身份运行终端，输入：
>
>    ```shell
>    reg delete HKEY_LOCAL_MACHINE\SOFTWARE\Classes\Drive\shell\WSL /f
>    reg delete HKEY_LOCAL_MACHINE\SOFTWARE\Classes\Directory\background\shell\WSL /f
>    reg delete HKEY_LOCAL_MACHINE\SOFTWARE\Classes\Directory\shell\WSL /f
>                
>    ```
>
>    执行完毕后问题解决。
>



## 终端自动安装 

### 常规步骤

1. 首先请确保你的Windows版本大于Windows10 2004（内部版本号19041）。如果你没有微软应用商店，可能会出错，请转至**问题汇总-LTSC**

2. 执行命令

   ```shell
   wsl --install
   ```

3. 该指令将会自动启用Windows相关功能并给你安装Ubuntu的最新LTS发行版。如果你不想安装Ubuntu，可以使用以下指令

   ```shell
   wsl --install --no-distribution		#安装WSL但是不带任何发行版
   wsl --list --online		#列出所有可用的发行版
   wsl --install <发行版名称>	#安装选定的发行版
   ```

4. 安装完成以后使用 `wsl -l -v`来查看安装的发行版，显示应该和上文中图片一样。

### 问题汇总：

> 1. Windows 10 LTSC版在安装时因为没有微软应用商店可能会出现各种乱七八糟的问题。为了解决这个问题，我暂且提供三种方法。
>
>    - 使用`wsreset -i`命令直接重置微软应用商店，稍后他会自动安装。
>
>    - 在第一行命令的末尾加上 `--inbox`，此命令将使用Windows更新来安装WSL而不是微软应用商店。<span style="color:red">**注意：此命令将会开启Windows更新，如果你此前禁用了Windows更新，将会失效。**</span>
>
>      在第三行命令末尾加上`--web-download`，此命令将从网络下载而不是从Microsoft Store，但需要**良好的网络环境**。
>
>    - 使用下文的手动安装方法。
>
> 2. 在安装发行版的时候，LTSC版本也会因为没有微软应用商店而出很多错误。例如：在使用 `wsl --update`的时候也会出现一大堆bug，请使用 `--web-download`参数来从网络下载而不是从Microsoft Store。因此强烈建议使用 `wsreset -i`安装微软应用商店。~~你如果是“极客”当我没说。~~



## 手动安装教程

### 常规步骤

1. 检查自己的系统版本是否为：

   x64系统：1903 或更高版本（内部版本为 18362.1049 ）

   ARM系统：2004 或更高版本（内部版本为 19041）

   <span style="color:red">**请勿问出例如：“如何在不支持的系统上安装WSL这种系统级组件”这种弱智问题，你要是能做到可以去参与日本的Windows2000 Modernization计划**</span>

2. 输入以下命令以启用Windows的虚拟机服务和WSL服务

   ```shell
   dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
   dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
   ```

3. 下载WSL2的安装包

   - [适用于 x64 计算机的 WSL2 Linux 内核更新包](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)
   -  [适用于ARM计算机的 WSL2 Linux 内核更新包](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_arm64.msi)
   - 此处的链接可能会过时，若想安装最新版或者链接失效，请访问：https://learn.microsoft.com/zh-cn/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package

4. 将WSL2设置为默认

   ```shell
   wsl --set-default-version 2
   ```

5. 下载发行版 .appx 安装包

   > - [Ubuntu](https://aka.ms/wslubuntu)
   > - [Ubuntu 24.04](https://wslstorestorage.blob.core.windows.net/wslblob/Ubuntu2404-240425.AppxBundle)
   > - [Ubuntu 22.04 LTS](https://aka.ms/wslubuntu2204)
   > - [Ubuntu 20.04](https://aka.ms/wslubuntu2004)
   > - [Ubuntu 20.04 ARM](https://aka.ms/wslubuntu2004arm)
   > - [Ubuntu 18.04](https://aka.ms/wsl-ubuntu-1804)
   > - [Ubuntu 18.04 ARM](https://aka.ms/wsl-ubuntu-1804-arm)
   > - [Ubuntu 16.04](https://aka.ms/wsl-ubuntu-1604)
   > - [Debian GNU/Linux](https://aka.ms/wsl-debian-gnulinux)
   > - [Kali Linux](https://aka.ms/wsl-kali-linux-new)
   > - [SUSE Linux Enterprise Server 12](https://aka.ms/wsl-sles-12)
   > - [SUSE Linux Enterprise Server 15 SP2](https://aka.ms/wsl-SUSELinuxEnterpriseServer15SP2)
   > - [SUSE Linux Enterprise Server 15 SP3](https://aka.ms/wsl-SUSELinuxEnterpriseServer15SP3)
   > - [openSUSE Tumbleweed](https://aka.ms/wsl-opensuse-tumbleweed)
   > - [openSUSE Leap 15.3](https://aka.ms/wsl-opensuseleap15-3)
   > - [openSUSE Leap 15.2](https://aka.ms/wsl-opensuseleap15-2)
   > - [Oracle Linux 8.5](https://aka.ms/wsl-oraclelinux-8-5)
   > - [Oracle Linux 7.9](https://aka.ms/wsl-oraclelinux-7-9)
   > - [Fedora Remix for WSL](https://github.com/WhitewaterFoundry/WSLFedoraRemix/releases/)

6. 打开Windows Powershell（或者其他什么的终端也行），切换到 .appx 包所在的目录并运行：

   ```shell
   Add-AppxPackage .\<包名>.appx
   ```

7. 等待安装完成后可以输入 `wsl -l -v`查看是否安装完成。

### 问题汇总

1. 在执行 `wsl --update`的时候可能会报错，请使用 `--web-download`参数来从网络下载而不是从Microsoft Store。
2. 步骤二以后如果无法安装WSL2的msi包可以尝试重启

## WSL常用命令汇总

```shell
# 安装WSL并指定Linux发行版
wsl --install  # 默认安装Ubuntu
 --distribution <发行版名称>：指定安装的发行版
 --no-launch：安装后不自动启动
 --web-download：在线下载安装
 --inbox：使用Windows组件安装WSL（非Microsoft Store）
 --enable-wsl1：启用WSL 1组件
 --no-distribution：不安装任何发行版

# 查看在线可用发行版列表
wsl --list --online  # 别名：wsl -l -o

# 查看已安装的Linux发行版列表及状态
wsl --list --verbose  # 别名：wsl -l -v
 --all：列出所有发行版
 --running：仅列出当前运行的发行版
 --quiet：仅显示发行版名称

# 将指定发行版设置为WSL1或WSL2
wsl --set-version <发行版名称> <1/2>  # 切换WSL版本

# 设置WSL默认版本
wsl --set-default-version <1/2>

# 设置默认Linux发行版
wsl --set-default <发行版名称>

# 将目录切换至主目录
wsl ~  # 启动WSL并切换至主目录

# 以指定用户身份运行特定发行版
wsl --distribution <发行版名称> --user <用户名>


# 更新WSL至最新版本
wsl --update
 --web-download：从GitHub而非Microsoft Store下载更新

# 检查WSL状态
wsl --status

# 检查WSL版本
wsl --version

# 帮助命令
wsl --help

# 以特定用户身份运行WSL
wsl --user <用户名>

# 更改发行版默认用户
<发行版名称> config --default-user <用户名>

# 关闭所有运行的WSL进程
wsl --shutdown  

# 终止指定发行版
wsl --terminate <发行版名称>

# 获取WSL 2安装的Linux发行版IP地址
wsl hostname -I  

# 导出发行版
wsl --export <发行版名称> <文件名>  
 --vhd：导出为.vhdx文件（仅WSL2支持）

# 导入发行版
wsl --import <发行版名称> <安装路径> <文件名>  
 --vhd：导入.vhdx文件
 --version <1/2>：导入WSL1或WSL2

# 即时导入VHDX文件作为发行版
wsl --import-in-place <发行版名称> <文件名>

# 注销或卸载发行版
wsl --unregister <发行版名称>

# 挂载磁盘至WSL
wsl --mount <磁盘路径>
 --vhd：虚拟硬盘
 --name <名称>：挂载点名称
 --bare：仅附加磁盘，不挂载
 --type <文件系统类型>：文件系统类型
 --partition <分区号>：指定挂载分区
 --options <挂载选项>：特定文件系统的挂载选项

# 卸载磁盘
wsl --unmount <磁盘路径>  

```

