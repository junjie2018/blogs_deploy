## 操作步骤

1. 指令如下：

~~~ shell
git config --global credential.helper store

sudo tee ~/.git-credentials <<-'EOF'
https://user:password@gitee.com
EOF
~~~