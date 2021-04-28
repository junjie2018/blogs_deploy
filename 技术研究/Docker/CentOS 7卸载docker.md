之所以选择卸载Docker，是因为我觉得简单工具的安装使用Docker只是提供了安装便利性，工具运行时并没有直接安装在物理机或虚拟机上那么高性能（直觉，未验证）。

~~~

yum list installed | grep docker

# 未验证这种通配法可以不，我是一个一个删除的
yum -y remove docker*

rm -rf /var/lib/docker

~~~

## 参考资料

1. [https://blog.csdn.net/liujingqiu/article/details/74783780](Centos 7 如何卸载docker)