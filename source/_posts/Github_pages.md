---
title: Github pages 使用
---

## 介绍

**Github Pages 是**面向用户、组织和项目开放的公共静态页面搭建托管服务，站点可以被免费托管在**Github** 上，你可以选择使用**Github Pages** 默认提供的域名**github**.**io**或者自定义域名来发布站点。 

## 入门四部曲

1. 学会git (前提)
     可以参考 [廖雪峰的教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
       git进阶: << Pro Git >>

2. 尝试使用github pages.   

     (下文 section one) 

  新建repo: yourname.github.io 

  在这个库下的master分支存放网页文件来使用github pages
  如果你已经有了自己的静态网页,那么到这里你就完成你的目标了

3. 使用hexo生成静态网页

     (下文 section two)

     如果不想自己编写html,可以使用hexo把markdown文件专程html. 并且hexo提供了丰富的主题模板
       这步参考 [hexo官网](https://hexo.io/zh-cn/index.html)

4. 将hexo源码和网页同时使用github保存.

     (下文section three)


## section one
在github 新建repo:yourname.github.io 在此repo里面的内容就可以在xxx.github.io中打开.

可以参考https://segmentfault.com/a/1190000011535121

首先得知道Github pages的规则：每个Github账号（比如Username）下面只能建立一个Pages，且命名必须符合这样的规则："username/username.github.io"

创建成功后，username.github.io就是你的域名（当然你可以通过别名解析绑定自己的域名）

实战：

1， 在Github建立一个新的Repository：命名为：username.github.io

2， 本地clone仓库：

```shell
git clone https://github.com/username/username.github.io
```

3， 进入文件夹，新建index.html

```shell
cd username.github.io 
echo "Hello World" > index.html
```

4， 执行命令：

```shell
git add .
git commit -m "Initial commit"
git push -u origin master
```

然后访问username.github.io，大功告成！

yourname.github.io形式的库，会解析master分支；而别的名字的库，会解析gh-pages分支，以yourname.github.io/库名的形式访问。因此可以在github pages 里面新建多个网站.  

## section two: 使用Hexo 

除了这样自己编写网页文件,也可以使用hexo / jekyll 将你写的markdown文档自动转成风格一致的静态网页.

推荐看[官方文档](https://hexo.io/zh-cn/docs/setup).

### hexo 安装

使用 hexo 需要先安装 Node.js.   

```shell
wget -qO- https://raw.github.com/creationix/nvm/master/install.sh | sh  
# then restart terminal 
nvm install stable
npm install -g hexo-cli 
```

### hexo 使用

不同的人使用hexo也有不同的习惯

#### 1.在本地使用hexo生成网页,deploy到master.
按照hexo官方文档: https://hexo.io/zh-cn/docs/commands

   自己新建一个文件夹,在这个文件夹下
```
$ hexo init <folder>
$ cd <folder>
$ npm install
```
##### 安装主题,如 next
```
git clone https://github.com/iissnan/hexo-theme-next.git themes/hexo-theme-next
```
其次，在_config.yml文件中配置主题。
```
theme: hexo-theme-next
```
编辑好_config.yml后可以使用 

```
hexo g
hexo s
```
来查看生成网页,并且在一在localhost:4000下查看网页

使用 hexo-deployer-git插件可以 把网页文件直接部署到github上,相关配置也在 _config.yml 下编辑
这会很方便的直接把本地生成的 public 文件夹(网页文件所在) 上传到github, 就可以直接在github.io上访问了.
```
npm install hexo-deployer-git --save
hexo d
```
这个方式是官方的,顺着官方的网页很容易就完成了.但是你的本地源码需要自己保存好

## section three: 同时上传源码与网页到github
### 1. 源码保存在分支,网页部署到yourname.github.io的master
这可以将你的的源码也保存到github上 参考:https://segmentfault.com/a/1190000011535121
先新建一个repo:yourname.github.io, clone到本地后, 新建并进入分支  git checkout -b source
hexo init 生成 hexo文件(先移出.git,完成后再移入).
再这个repo下的source分支如上使用hexo产生网页,并deploy到master分支. 
这样 master分支是网页, source 分支是源码. 同时备份上传到同一repo下.

### 2. 源码保存在master分支,网页部署到gh-pages
利用gh-pages分支   可以参考:https://juejin.im/post/5acf02086fb9a028b92d8652
非yourname.github.io的repo，如果有gh-pages分支，那么其中的网页可以以yourname.github.io/repo_name的形式访问
所以完全可以用类似2一样的方式组织代码和网页.
在github上新建repo,如 note.  clone到本地.
移出.git后 hexo init ,再移入.git
现在的hexo init 是在master 分支下. 
```
git add .
git commit -m 'hexo init'
```
然后同样的步骤 安装 主题,编辑 _config.yml
```
deploy:
  type: git
  repo: <repository url> #库（Repository）地址
  branch: gh-pages
  message: [message]
```
之后 使用 hexo d 部署网页到 gh-pages分支下.
源码 可以 push 到 这个repo的msater下.
在  yourname.github.io/note/ 下就可以看到 deploy 的网页.

## 总结
1. 使用pages的方式很简单. 将网页放到yourname.github.io库的master分支或者其他库的gh-pages分支就完成了网页部署.
2. 使用hexo可以在本地方便的将markdown转换成网页. hexo有丰富的网页模板.
3. 利用hexo的插件hexo-deployer-git,可以直接将网页部署到github上. 具体位置在_config.yml上.
4. 祝玩的开心!













