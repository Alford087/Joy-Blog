> iOS 逆向学习笔记：OpenSSH 的原理和使用方法

##  SSH 协议
SSH（Secure Shell）是一种能够以安全的方式提供远程登录的协议，也是目前远程管理 Linux 系统的首选方式。

在 iOS 逆向开发中，最常用的命令是
```
ssh user@host
```

在 iOS 越狱开发中，常用的 user 是 root 用户和 mobile 用户

* root：系统中最高权限的账户，具有对系统完全的控制权
* mobile：普通用户，可以操作一些普通的文件，但系统文件不可操作

## OpenSSH

SSH 只是一种协议，存在多种实现，既有商业实现，也有开源实现。OpenSSH 就是其中一种常用的 SSH 实现。Cydia 的作者 Saurik 把 OpenSSH 这一软件移植到了 iOS 平台上，并且简化了安全认证密钥的繁琐，使之成为一款可以在iPhone上运行的Cydia插件。通过 OpenSSH 就可以在 Mac 上远程输入命令操作 iOS 设备。

## 如何保证安全？

* 密码登陆：公钥加密，同时为了预防中间人攻击，使用了口令登陆，让主机的连接者自己去校验公钥是否正确，从而避免中间人的攻击。
* 公钥登陆：就是用户将自己的公钥储存在远程主机上。登录的时候，远程主机会向用户发送一段随机字符串，用户用自己的私钥加密后，再发回来。远程主机用事先储存的公钥进行解密，如果成功，就证明用户是可信的，直接允许登录shell，不再要求密码。

该段参考自阮一峰的 [SSH原理与运用（一）：远程登录](http://www.ruanyifeng.com/blog/2011/12/ssh_remote_login.html)，里面详细的介绍如何保证安全。

## 免密码登陆（公钥登陆）

* 可以参考 [配置ssh密钥认证自动登录](https://segmentfault.com/a/1190000000481249)

## 远程传输命令
scp（secure copy）是一个基于 SSH 协议在网络之间进行安全传输的命令，其格式为 “scp [参数] 本地文件 远程帐户@远程IP地址:远程目录”。


