## 操作步骤

1. 准备配置文件

~~~ shell

mkdir -p /home/junjie/mysql/conf
mkdir -p /home/junjie/mysql/logs
mkdir -p /home/junjie/mysql/mysql

tee /home/junjie/mysql/conf/my.cnf <<-'EOF'
[client]
default-character-set=utf8mb4
[mysql]
default-character-set=utf8mb4
[mysqld]
sql-mode=STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION
character-set-server=utf8mb4
EOF

~~~

2. 启动docker

~~~ shell

sudo docker run \
    --restart always -p 3306:3306 \
    --name mysql \
    -v /home/junjie/mysql/conf/my.cnf:/etc/mysql/my.cnf \
    -v /home/junjie/mysql/logs:/logs \
    -v /home/junjie/mysql/mysql:/var/lib/mysql \
    -e MYSQL_ROOT_PASSWORD=root \
    -d mysql:5.7.31

~~~

## 相关教程

1. [docker 安装 mysql5.7](https://www.cnblogs.com/binz/p/12295374.html)