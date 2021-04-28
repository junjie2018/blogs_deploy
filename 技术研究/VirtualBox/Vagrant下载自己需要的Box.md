我刚接触Vagrant时，官方Box搜索页面是不提供任何下载按钮的，需要一些特殊的技巧得到下载链接。我最近发现官方提供了下载按钮，满心欢喜的去尝试，结果下载到一半的时候速度降到非常低，而且还出现400错误，头疼。

下面的教程我目前使用时，还是没有任何问题的。

## 操作步骤

1. 在[Discover Vagrant Boxes](https://app.vagrantup.com/boxes/search)搜索你需要的box，然后进入该box的详情页，随便选择一个版本，进入该版本的详情页，如下所示：

![2021-04-11-10-43-08](https://junjie2018sz.oss-cn-shenzhen.aliyuncs.com/images/2021-04-11-10-43-08.png)

2. 在地址栏中加入`/providers/virtualbox.box`，得到下载地址（virtualbox.box可以换成你自己的环境），可以将下载地址复制到自己的下载器中下载。

~~~

https://app.vagrantup.com/generic/boxes/centos8/versions/3.2.14/providers/virtualbox.box

~~~

3. 下载文件拖动到Centos中，改一个名字，然后执行如下代码加载：

~~~

vagrant box add --name BOX_NAME FILE_NAME

~~~