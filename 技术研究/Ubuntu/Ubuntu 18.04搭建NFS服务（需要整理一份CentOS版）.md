## 操作步骤

### 服务端

1. 指令如下：

~~~ shell
sudo apt install nfs-kernel-server

sudo mkdir -p ~/nfs
sudo chown nobody:nogroup ~/nfs
sudo chmod 777 ~/nfs


sudo tee /etc/apt/sources.list <<-'EOF'
/home/junjie/nfs *(insecure,rw,sync,no_subtree_check)
EOF

sudo exportfs -a
sudo systemctl restart nfs-kernel-server
~~~

### 客户端

1. 指令如下

~~~ shell
sudo apt-get install nfs-common

sudo mkdir -p ~/nfs_client

sudo mount 192.168.30.174:/home/junjie/nfs /home/vagrant/nfs_client
~~~

## 相关教程

1. [10分钟学会在Ubuntu 18.04 LTS上安装NFS服务器和客户端](https://www.linuxidc.com/Linux/2018-11/155331.htm)
2. [mount.nfs: access denied by server while mounting 一个解决办法](https://blog.csdn.net/zhanzheng520/article/details/19966383/)