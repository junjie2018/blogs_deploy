## 问题描述

1. 执行如下VBoxManage --version，报如下错误：

~~~

WARNING: The vboxdrv kernel module is not loaded. Either there is no module
         available for the current kernel (4.18.0-240.el8.x86_64) or it failed to
         load. Please recompile the kernel module and install it by

           sudo /sbin/vboxconfig

         You will not be able to start VMs until this problem is fixed.
6.1.18r142142


~~~

## 解决步骤

1. 执行sudo /sbin/vboxconfig后，有如下提示（这不是完整的提示，是我修复了一部分问题后的提示，仅做参考）：

~~~ 

This system is currently not set up to build kernel modules.
Please install the Linux kernel "header" files matching the current kernel
for adding new hardware support to the system.
The distribution packages containing the headers are probably:
    kernel-devel kernel-devel-4.18.0-240.el8.x86_64
This system is currently not set up to build kernel modules.
Please install the Linux kernel "header" files matching the current kernel
for adding new hardware support to the system.
The distribution packages containing the headers are probably:
    kernel-devel kernel-devel-4.18.0-240.el8.x86_64

There were problems setting up VirtualBox.  To re-start the set-up process, run
  /sbin/vboxconfig
as root.  If your system is using EFI Secure Boot you may need to sign the
kernel modules (vboxdrv, vboxnetflt, vboxnetadp, vboxpci) before you can load
them. Please see your Linux system's documentation for more information.


~~~

2. 按照提示安装相应的软件包，具体安装的软件包有（建议按照提示做，仔细读提示，会告诉你缺少哪些软件包）：

~~~

dnf install -y gcc make perl
dnf install -y kernel-devel

~~~

3. 完成如上工作后执行sudo /sbin/vboxconfig依旧报如下错误，仍然提示是kernel-devel的错误，我仔细对比后发现，执行dnf install -y kernel-devel后安装的为kernel-devel-4.18.0-240.22.1.el8_3.x86_64，但是这个和我内核的对不上，我实际上需求为：kernel-devel-4.18.0-240.el8.x86_64。

~~~

vboxdrv.sh: Stopping VirtualBox services.
vboxdrv.sh: Starting VirtualBox services.
vboxdrv.sh: Building VirtualBox kernel modules.
This system is currently not set up to build kernel modules.
Please install the Linux kernel "header" files matching the current kernel
for adding new hardware support to the system.
The distribution packages containing the headers are probably:
    kernel-devel kernel-devel-4.18.0-240.el8.x86_64
This system is currently not set up to build kernel modules.
Please install the Linux kernel "header" files matching the current kernel
for adding new hardware support to the system.
The distribution packages containing the headers are probably:
    kernel-devel kernel-devel-4.18.0-240.el8.x86_64

There were problems setting up VirtualBox.  To re-start the set-up process, run
  /sbin/vboxconfig
as root.  If your system is using EFI Secure Boot you may need to sign the
kernel modules (vboxdrv, vboxnetflt, vboxnetadp, vboxpci) before you can load
them. Please see your Linux system's documentation for more information.

~~~

4. 如何处理该问题，我选择去官网手动下载该软件包，拖到服务器后，执行如下指令安装：

~~~

# 软件包下载地址
http://mirror.centos.org/centos/8/BaseOS/x86_64/os/Packages/

dnf -y install kernel-devel-4.18.0-240.el8.x86_64.rpm

~~~

5. 解决该问题后，执行/sbin/vboxconfig有如下报错，并按照报错查看日志文件有，所以按照日志文件中的提示我又安装了一部分软件：

~~~

# 报错

vboxdrv.sh: Stopping VirtualBox services.
vboxdrv.sh: Starting VirtualBox services.
vboxdrv.sh: Building VirtualBox kernel modules.
vboxdrv.sh: failed: Look at /var/log/vbox-setup.log to find out what went wrong.

There were problems setting up VirtualBox.  To re-start the set-up process, run
  /sbin/vboxconfig
as root.  If your system is using EFI Secure Boot you may need to sign the
kernel modules (vboxdrv, vboxnetflt, vboxnetadp, vboxpci) before you can load
them. Please see your Linux system's documentation for more information.
[root@3400g KernelDevel]# cat/var/log/vbox-setup.log
-bash: cat/var/log/vbox-setup.log: No such file or directory


# 日志文件

Building the main VirtualBox module.
Error building the module:
make V=1 CONFIG_MODULE_SIG= CONFIG_MODULE_SIG_ALL= -C /lib/modules/4.18.0-240.el8.x86_64/build M=/tmp/vbox.0 SRCROOT=/tmp/vbox.0 -j8 modules
make[1]: warning: -jN forced in submake: disabling jobserver mode.
Makefile:978: *** "Cannot generate ORC metadata for CONFIG_UNWINDER_ORC=y, please install libelf-dev, libelf-devel or elfutils-libelf-devel".  Stop.
make: *** [/tmp/vbox.0/Makefile-footer.gmk:117: vboxdrv] Error 2


# 安装的软件包

dnf -y install elfutils-libelf-devel

~~~

6. 完成如上步骤后，再次执行/sbin/vboxconfig，一路顺顺利利的完成任务了。哈哈，终于拨开云雾见日明，可喜可贺。

~~~

[root@3400g ~]# VBoxManage --version
6.1.18r142142

~~~

## 个人小结

之前用Ubuntu时，确实在这些方面没有遇到过这么多问题。但是在解决CentOS的问题时，我需要查的资料数量远远小于Ubuntu，查到的很多资料都是可用的，像我解决的这个问题，甚至在日志信息中都给了足够的解决方案。

这次我CentOS、VirtualBox和Vagrant都使用了最新版，遇到问题在所难免，但是我感觉这样才有意思，哈哈。
