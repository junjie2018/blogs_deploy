3.15号博文

## 问题描述

在导入项目时，我按下图配置了Maven，同时我的setting.xml文件是从我同事那要的。结果我项目中多处报红。

## 解决步骤

修改setting.xml文件中如下标签，该标签需要与在Idea中配置位置对应。

~~~ xml

<localRepository>D:\MavenRepository\repository</localRepository>

~~~