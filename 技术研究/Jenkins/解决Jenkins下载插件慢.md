## 解决步骤

1. 修改插件源为：

~~~
https://mirrors.tuna.tsinghua.edu.cn/jenkins/updates/update-center.json
~~~

2. 修改updates/default.json文件：
    - updates.jenkins-ci.org/download修改为：mirrors.tuna.tsinghua.edu.cn/jenkins
    - www.google.com修改为：www.baidu.com

3. 重启Jenkins

## 相关教程

1. [【Jenkins】插件更改国内源](https://www.cnblogs.com/suzy/p/12665728.html)