## 问题现象

1. 执行hexo generate时出现了如下警告，且首页无法访问（空白的）

~~~
WARN  No layout: 404.html
WARN  No layout: categories/index.html
WARN  No layout: search/index.html
WARN  No layout: post/Git客户端修改默认的编辑器.html
WARN  No layout: post/使用Docker快速启动一个MySQL实例.html
WARN  No layout: post/使用Docker快速启动一个RabbitMQ实例.html
WARN  No layout: post/设置Docker容器加速及允许通过http协议拉取镜像.html
~~~

## 解决方法

1. 检查themes下的主题目录与_config.yml配置文件中的theme的值是否对应
2. 检查themes下的主题文件夹中的内容是否完成（我的项目中是因为这个问题导致的）

## 问题小结

这是一个很有趣的问题，我在我Windows机器上在themes文件夹拉下了主题文件，然后将这个项目提交到git仓库中。然后我去到我Linux机器中拉下代码，hexo generate该项目，结果就出现了这个问题。

真正的问题在于，我提交项目时，从GitHub拉下来的主题文件并没有正常的提交到仓库，甚至使用git status时，总是提示没有任何文件更新。

发现问题后，解决问题反倒变得简单，我删除了该主题文件，然后使用git add -A && git commit -m ""重新提交了一次（即[目录下增加了文件，git感知不到的规避办法]）。然后重新拉取主题文件，并删除其中的.git文件夹（这一步，我不确实是否必须这么做）。

## 相关教程

1. [目录下增加了文件，git感知不到的规避办法]
2. [hexo本地测试运行重启后页面空白,提示 : WARN No layout: index.html?](https://www.zhihu.com/question/38781463)

## 其他资源

1. [thinkerchan/hexo-theme-greyshade](https://github.com/thinkerchan/hexo-theme-greyshade)
2. [有哪些好看的 Hexo 主题？](https://www.zhihu.com/question/24422335/answers/updated)
3. [修改git默认的编辑器](https://blog.csdn.net/qwaszx523/article/details/79622844)

[目录下增加了文件，git感知不到的规避办法]:(https://blog.csdn.net/weixin_34332905/article/details/92930275)