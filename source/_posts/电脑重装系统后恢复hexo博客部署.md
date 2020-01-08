装系统之前先备份一下自己的hexo博客文件夹，现在就是借助这些文件恢复部署一下就好了。具体方法如下：

一、安装 node.js 和 git for windows

~~~zsh
$ apt install nodejs
$ apt install git
~~~

二、配置 git 个人信息，生成新的 ssh 密钥

<!-- more -->

```
git config --global user.name "zalmon-sources"
git config --global user.email "zalmon@gmail.com"
ssh-keygen -t rsa -C "zalmon@gmail.com"
```

你需要把邮件地址和用户名换成你自己的，然后一路回车，使用默认值即可。

如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，打开id_rsa.pub文件，复制里面的内容。

三、将生成的ssh公钥（刚复制的内容）复制到Github的settings里面的ssh选项里去

https://github.com/settings/keys

四、安装hexo：

```
npm install hexo-cli -g
```

五、打开原来的hexo博客所在文件夹，只需保留_config.yml，theme/，source/，scaffolds/，package.json，.gitignore 这些项目，删除其他的文件。

六、然后打开 git bush 运行命令：

```
npm install
```

七、安装部署插件：

```
npm install hexo-deployer-git --save //hexo d 部署到git插件
```

八、接下来直接hexo g hexo d试一下是否成功。

```
hexo g
hexo d
```

博客部署恢复完成。

## Hexo部署过程中的难点解决：

1、如果博客有RSS订阅和站点地图功能，请在第七步安装下面两个插件，命令如下：

```
npm install hexo-generator-feed --save  //RSS订阅插件
npm install hexo-generator-sitemap --save //站点地图插件
```

2、安装部署过程中，在git bash中使用hexo g或者hexo d等命令，会报错提示： Cannot find module ‘C:\Program Files\Git\node_modules\hexo-cli\bin\hexo’。

如图所示：

![photo](https://i.loli.net/2019/05/09/5cd447d94e80a.jpg)

我当时的解决办法：
在C盘用户目录下，找到这个文件夹：C:\Users\Administrator\AppData\Roaming\npm\node_modules\hexo-cli。
然后把node_modules这个文件夹复制到Git安装目录下（C:\Program Files\Git）即可。

3、怎么用hexo上传一个README.md到github?
因为README.md文件一执行hexo d命令之后，README文件就被渲染变为README.html文件。

解决办法：
在Hexo目录下的source根目录下添加一个 [README.md](http://readme.md/)；
修改Hexo目录下的_config.yml，设置 skip_render: README.md保存退出即可；
使用hexo d 命令就不会再渲染 [README.md](http://readme.md/) 这个文件了。

原博文链接：[重装系统后，Hexo博客如何重新部署恢复](https://helloqingfeng.github.io/2017/02/25/hexo-rebuilding/)