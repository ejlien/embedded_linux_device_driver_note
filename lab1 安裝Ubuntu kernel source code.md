---
tags: Linux, Linux Device Driver
--- 

[TOC]

# lab1 安裝 Ubuntu kernel source 
1. 查詢 ubuntu kernel version
```
    uname -r
```    
```shell=
avatar@avatar-VirtualBox:~$ uname -r
4.15.0-133-generic
```

2. 更新軟體套件清單 
   更新我們的套件清單 /etc/apt/sources.list，這樣在我們更新時才能比對最新的套件清單，決定是否更新
```
sudo apt-get update -y
```

:::info
-y, --yes, --assume-yes
           Automatic yes to prompts; assume "yes" as answer to all prompts and
           run non-interactively. If an undesirable situation, such as
           changing a held package, trying to install a unauthenticated
           package or removing an essential package occurs then apt-get will
           abort. Configuration Item: APT::Get::Assume-Yes.  
:::


```shell=
avatar@avatar-VirtualBox:~$ sudo apt-get update -y
[sudo] password for avatar: 
Hit:1 http://tw.archive.ubuntu.com/ubuntu xenial InRelease
Hit:2 http://tw.archive.ubuntu.com/ubuntu xenial-updates InRelease                   
Hit:3 http://tw.archive.ubuntu.com/ubuntu xenial-backports InRelease                 
Ign:4 http://archive.canonical.com natty InRelease                                   
Hit:5 http://security.ubuntu.com/ubuntu xenial-security InRelease           
Ign:6 http://archive.canonical.com natty Release  
Ign:7 http://archive.canonical.com natty/partner amd64 Packages.diff/Index
Ign:8 http://archive.canonical.com natty/partner i386 Packages.diff/Index
Ign:9 http://archive.canonical.com natty/partner all Packages
Ign:10 http://archive.canonical.com natty/partner Translation-en_US
Ign:11 http://archive.canonical.com natty/partner Translation-en
Ign:12 http://archive.canonical.com natty/partner amd64 DEP-11 Metadata
Ign:13 http://archive.canonical.com natty/partner DEP-11 64x64 Icons
Ign:14 http://archive.canonical.com natty/partner amd64 Packages
Ign:15 http://archive.canonical.com natty/partner i386 Packages
Ign:9 http://archive.canonical.com natty/partner all Packages
Ign:10 http://archive.canonical.com natty/partner Translation-en_US
Ign:11 http://archive.canonical.com natty/partner Translation-en
Ign:12 http://archive.canonical.com natty/partner amd64 DEP-11 Metadata
Ign:13 http://archive.canonical.com natty/partner DEP-11 64x64 Icons
Ign:14 http://archive.canonical.com natty/partner amd64 Packages
Ign:15 http://archive.canonical.com natty/partner i386 Packages
Ign:9 http://archive.canonical.com natty/partner all Packages
Ign:10 http://archive.canonical.com natty/partner Translation-en_US
Ign:11 http://archive.canonical.com natty/partner Translation-en
Ign:12 http://archive.canonical.com natty/partner amd64 DEP-11 Metadata
Ign:13 http://archive.canonical.com natty/partner DEP-11 64x64 Icons
Ign:14 http://archive.canonical.com natty/partner amd64 Packages
Ign:15 http://archive.canonical.com natty/partner i386 Packages
Ign:9 http://archive.canonical.com natty/partner all Packages
Ign:10 http://archive.canonical.com natty/partner Translation-en_US
Ign:11 http://archive.canonical.com natty/partner Translation-en
Ign:12 http://archive.canonical.com natty/partner amd64 DEP-11 Metadata
Ign:13 http://archive.canonical.com natty/partner DEP-11 64x64 Icons
Ign:14 http://archive.canonical.com natty/partner amd64 Packages
Ign:15 http://archive.canonical.com natty/partner i386 Packages
Ign:9 http://archive.canonical.com natty/partner all Packages
Ign:10 http://archive.canonical.com natty/partner Translation-en_US
Ign:11 http://archive.canonical.com natty/partner Translation-en
Ign:12 http://archive.canonical.com natty/partner amd64 DEP-11 Metadata
Ign:13 http://archive.canonical.com natty/partner DEP-11 64x64 Icons
Ign:14 http://archive.canonical.com natty/partner amd64 Packages
Ign:15 http://archive.canonical.com natty/partner i386 Packages
Ign:9 http://archive.canonical.com natty/partner all Packages
Ign:10 http://archive.canonical.com natty/partner Translation-en_US
Ign:11 http://archive.canonical.com natty/partner Translation-en
Ign:12 http://archive.canonical.com natty/partner amd64 DEP-11 Metadata
Ign:13 http://archive.canonical.com natty/partner DEP-11 64x64 Icons
Err:14 http://archive.canonical.com natty/partner amd64 Packages
  404  Not Found [IP: 91.189.91.15 80]
Ign:15 http://archive.canonical.com natty/partner i386 Packages
Reading package lists... Done
W: The repository 'http://archive.canonical.com natty Release' does not have a Release file.
N: Data from such a repository can't be authenticated and is therefore potentially dangerous to use.
N: See apt-secure(8) manpage for repository creation and user configuration details.
E: Failed to fetch http://archive.canonical.com/dists/natty/partner/binary-amd64/Packages  404  Not Found [IP: 91.189.91.15 80]
E: Some index files failed to download. They have been ignored, or old ones used instead.

```

3. 安裝 linux source 4.15.0

```
sudo apt-get install -y linux-source-4.15.0
```

4. 切換目錄，解開 linux kernel source code
```
    cd /usr/src
    sudo tar -jxvf linux-source-4.15.0.tar.bz2
    du -hc -d 0 linux-source-4.15.0
```

```
avatar@avatar-VirtualBox:/usr/src$ ll
total 28
drwxr-xr-x  7 root root 4096 Feb  9 16:24 ./
drwxr-xr-x 14 root root 4096 Nov 27 09:48 ../
drwxr-xr-x 25 root root 4096 Jan 20 18:35 linux-headers-4.15.0-132/
drwxr-xr-x  8 root root 4096 Jan 20 18:35 linux-headers-4.15.0-132-generic/
drwxr-xr-x 25 root root 4096 Jan 31 09:59 linux-headers-4.15.0-133/
drwxr-xr-x  8 root root 4096 Jan 31 09:59 linux-headers-4.15.0-133-generic/
drwxrwxr-x 28 root root 4096 Jan 15 12:08 linux-source-4.15.0/
lrwxrwxrwx  1 root root   47 Jan 15 12:09 linux-source-4.15.0.tar.bz2 -> linux-source-4.15.0/linux-source-4.15.0.tar.bz2

```

```
avatar@avatar-VirtualBox:/usr/src$ tree -L 1 linux-source-4.15.0
linux-source-4.15.0
├── arch
├── block
├── certs
├── COPYING
├── CREDITS
├── crypto
├── debian
├── debian.hwe
├── debian.master
├── Documentation
├── drivers
├── dropped.txt
├── firmware
├── fs
├── include
├── init
├── ipc
├── Kbuild
├── Kconfig
├── kernel
├── lib
├── linux-source-4.15.0.tar.bz2
├── MAINTAINERS
├── Makefile
├── mm
├── net
├── README
├── samples
├── scripts
├── security
├── snapcraft.yaml
├── sound
├── tools
├── ubuntu
├── update-version-dkms
├── usr
└── virt

26 directories, 11 files

```

查看 linux-source-4.15.0 的全部檔案大小，du -hc -d 0 linux-source-4.15.0

```
avatar@avatar-VirtualBox:/usr/src$ du -hc -d 0 linux-source-4.15.0
1.1G	linux-source-4.15.0
1.1G	total
```

5. 若是要查看其他Ubutnu提供的 kernel source，可以用
```
sudo apt-cache search linux-source
```

可以看到 Ubutnu有提供以下發行的 kernel
```
avatar@avatar-VirtualBox:~$ sudo apt-cache search linux-source
[sudo] password for avatar: 
linux-source - Linux kernel source with Ubuntu patches
linux-source-4.4.0 - Linux kernel source for version 4.4.0 with Ubuntu patches
linux-source-4.10.0 - Linux kernel source for version 4.10.0 with Ubuntu patches
linux-source-4.11.0 - Linux kernel source for version 4.11.0 with Ubuntu patches
linux-source-4.13.0 - Linux kernel source for version 4.13.0 with Ubuntu patches
linux-source-4.15.0 - Linux kernel source for version 4.15.0 with Ubuntu patches
linux-source-4.8.0 - Linux kernel source for version 4.8.0 with Ubuntu patches

```

我們下載 4.4.0 版本的 kernel，但是並未下載成功，因為之前直接在 /usr/src 路徑下刪除了 linux-source-4.4.0 與 linux-source-4.4.0.tar.gz，需用正規的移除方式

```
sudo apt-get install linux-source-4.4.0
```

```
avatar@avatar-VirtualBox:~$ sudo apt-get install linux-source-4.4.0 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
linux-source-4.4.0 is already the newest version (4.4.0-201.233).
0 upgraded, 0 newly installed, 0 to remove and 24 not upgraded.

```

6. dpkg --list 'linux-source-*'

可以發現 linux-source-4.4.0 還在記錄內

```
avatar@avatar-VirtualBox:/usr/src$ dpkg --list 'linux-source-*'
Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Inst/Conf-files/Unpacked/halF-conf/Half-inst/trig-aWait/Trig-pend
|/ Err?=(none)/Reinst-required (Status,Err: uppercase=bad)
||/ Name                                      Version                   Architecture              Description
+++-=========================================-=========================-=========================-========================================================================================
un  linux-source-3                            <none>                    <none>                    (no description available)
ii  linux-source-4.15.0                       4.15.0-133.137~16.04.1    all                       Linux kernel source for version 4.15.0 with Ubuntu patches
ii  linux-source-4.4.0                        4.4.0-201.233             all                       Linux kernel source for version 4.4.0 with Ubuntu patches
ii  linux-source-4.8.0                        4.8.0-58.63~16.04.1       all                       Linux kernel source for version 4.8.0 with Ubuntu patches

```

7. 移除

sudo apt-get purge linux-source-4.4.0

```
avatar@avatar-VirtualBox:/usr/src$ sudo apt-get purge linux-source-4.4.0 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages will be REMOVED:
  linux-source* linux-source-4.4.0*
0 upgraded, 0 newly installed, 2 to remove and 25 not upgraded.
After this operation, 133 MB disk space will be freed.
Do you want to continue? [Y/n] y
(Reading database ... 236302 files and directories currently installed.)
Removing linux-source (4.4.0.201.207) ...
Removing linux-source-4.4.0 (4.4.0-201.233) ...

```

8. 再次查看

這次 linux-source-4.4.0 真的在名單上移除了
```
avatar@avatar-VirtualBox:/usr/src$ dpkg --list 'linux-source-*'
Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Inst/Conf-files/Unpacked/halF-conf/Half-inst/trig-aWait/Trig-pend
|/ Err?=(none)/Reinst-required (Status,Err: uppercase=bad)
||/ Name                                      Version                   Architecture              Description
+++-=========================================-=========================-=========================-========================================================================================
un  linux-source-3                            <none>                    <none>                    (no description available)
ii  linux-source-4.15.0                       4.15.0-133.137~16.04.1    all                       Linux kernel source for version 4.15.0 with Ubuntu patches
ii  linux-source-4.8.0                        4.8.0-58.63~16.04.1       all                       Linux kernel source for version 4.8.0 with Ubuntu patches

```
7. 可以download 的地方
    1. linux kernel 的網站
        https://www.kernel.org/
    2. ubuntu 的網站
        https://wiki.ubuntu.com/Kernel/BuildYourOwnKernel?_ga=2.205676179.1435408387.1654562073-1183088611.1654562073
    ubuntu 維護與發行的網站
    ???
  
8. reference: https://www.itread01.com/p/124808.html
9. 有時候會找不到此 source code
```
sudo apt-get install linux-source-$(uname -r)

avatar@avatar-VirtualBox:~$ sudo apt-get install linux-source-$(uname -r)
Reading package lists... Done
Building dependency tree       
Reading state information... Done
E: Unable to locate package linux-source-2.6.35-22-generic
E: Couldn't find any package by regex 'linux-source-2.6.35-22-generic'
```

## 小節
1. 查 kernel version
    uname -r
2. 下載
    sudo apt-get update -y
    sudo apt-get install linux-source-4.4.0
3. kernel source 安裝的路徑
    /usr/sre/linux-source-4.4.0
4. 檢查已安裝的 kernel
    dpkt --list 'linux-source-*'
5. 若要移除 kernel 安裝包
    sudo apt-get purge linux-source-4.4.0


## Error1, Could not get lock /var/lib/dpkg/lock-fronted...

### 訊息
當執行 sudo apt-get install linux-source-4.4.0 後，出現以下錯誤訊息

```avatar@avatar-VirtualBox:/usr/src$ sudo apt-get install linux-source-4.4.0
[sudo] password for avatar: 
E: Could not get lock /var/lib/dpkg/lock-frontend - open (11: Resource temporarily unavailable)
E: Unable to acquire the dpkg frontend lock (/var/lib/dpkg/lock-frontend), is another process using it?
```

### 解法
1. 等一會再執行相同的指令，因為一次只能有一個 apt 可以執行，若有第二個要執行，需要等待
2. 查看有哪個process也在執行 apt

```
ps aux | grep -i apt
```

```
avatar@avatar-VirtualBox:/usr/src$ ps aux | grep -i apt
root      2333  0.2  5.2 299980 106392 ?       SNl  09:18   0:00 /usr/bin/python3 /usr/sbin/aptd
avatar    2507  0.0  0.0  21572  1088 pts/3    S+   09:22   0:00 grep --color=auto -i apt
```
有一個 aptd 也在執行

3. 本次是等了一會 (約 5 min) 再次執行，就可以解決

4. 參考網址
https://phoenixnap.com/kb/fix-could-not-get-lock-error-ubuntu

