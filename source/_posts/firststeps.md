title: 博客搭建历程
tags: [git,npm, hexo, github]
categories: 博客搭建

---
> 折腾了差不多快一个星期了，总算把这个博客给鼓捣出来了，记录一下，帮助一下想要搭建的小伙伴！

## 源起
本来早就打算自己搭建个博客了，一来可以记录学习中遇到的各种问题，以防忘记；二来可以督促自己该学习了，别特么一天到晚就知道瞎扯淡，否则啥时候能买得起一套房，怎么对得起一直陪自己吃苦的女友；三来还可以打发空闲时间，岂不快哉！所以，也就有了这个博客的诞生。<!-- more -->

## 选型
虽然有了这个搭博客的想法，却一直纠结在博客页面布局上，我想要的是简洁，美观，高大上的类型，必须得自己搭建的博客。了解到现在的主流博客基本都是用Hexo、jekyll或者是express来搭建，或者借助于第三方的平台，比如CSDN，简书，头条等等。后来，偶然间在网上发现了一个博客，是用hexo+next搭建在github上的博客，满足了我的所有要求，简洁，炫酷，简直就是写博客的上选之作，于是，找了一些教程，说干就干...

## 详细步骤
### 搭建git环境

>点击[这里](https://git-for-windows.github.io/)download下载，然后next,next,next...

### hexo、next安装

>* 打开Git Bash，全局安装hexo：`npm install -g hexo`
* 定位到想要创建博客的路径上，运行命令：`hexo init`，创建搭建hexo博客需要的文件
* 安装npm依赖包：`npm install`
* 从github上拉next到博客路径：`git clone https://github.com/iissnan/hexo-theme-next themes/next`
* 修改博客配置文件youbolg/_config.yml，找到 ***theme*** 字段，并将其值更改为 ***next***，这样就把hexo的主题设置为next了
* 其他的基本设置请参考：[next官方文档](http://theme-next.iissnan.com/)

### 优化主题

> * 增加文章阅读时长，字数统计显示
安装： `npm i --save hexo-wordcount`
使用：搜索***leancloud-visitors-count*** 放到下面:
```html
 <span class="post-time">
    &nbsp; | &nbsp;
	<span class="post-meta-item-icon">
		<i class="fa fa-calendar-o"></i>
		</span>
		<span class="post-meta-item-text">字数统计:</span>
		<span class="post-count">{{ wordcount(post.content) }}(字)</span>
    </span>
    <span class="post-time">
		&nbsp; | &nbsp;
		<span class="post-meta-item-icon">
			<i class="fa fa-calendar-o"></i>
		</span>
		<span class="post-meta-item-text">阅读时长:</span>
		<span class="post-count">{{ min2read(post.content) }}(分)</span>
	</span>
</span> 
```

### 部署github
> * 登录github、创建repo(注意注册的名字必须和repo名字相同)参考链接：[kezhenxue](https://www.cnblogs.com/keZhenxu94/p/5288488.html)
* 获取并设置ssh key, 复制repo的https url复制到博客配置文件中：
` deploy:
  type: git
  repository: https://github.com/fuey/fuey.github.io.git
  branch: master
`
* 设置Git的username 和 email地址：
`git config --global user.name "xuhaiyan"`、`git config --global user.email "haiyan.xu.vip@gmail.com"`
* 检查ssh key，创建ssh key，设置ssh key
1. 在bash中，检查是否已经存在了SSH keys:`ls -al ~/.ssh`
2. 如果存在，到C:\Users\用户名\\.ssh路径下删除全部的文件
3. 获取到ssh key：`ssh-keygen -t rsa -C "youemailaddress@**.com"`,然后到C:\Users\用户名\\.ssh路径下看是否已经生成
4. 生成的话直接执行：`clip < ~/.ssh/id_rsa.pub`复制ssh key
5. 然后到刚才创建的repo下，setting->SSH keys->add SSH key ->填入title(随便填),key(直接Ctrl+v)。
6. 测试配置是否正确:`ssh -T git@github.com`，输入yes，看到successful，那么恭喜你也有了一个炫酷的博客了！

### 常用命令
> hexo c      #相当于 hexo clean  清除缓存
> hexo g      #相当于 hexo generate  生成解析过后的博客代码
> hexo s      #相当于 hexo server  本地服务
> hexo d      #相当于 hexo deploy  部署到设置的github或者coding

## 参考链接	
[next官方文档](http://theme-next.iissnan.com/) | [JORY'S BLOG](http://www.joryhe.com) | [Hexo theme list](https://hexo.io/themes/)  | [cnblogs](http://www.cnblogs.com/syd192/p/6074323.html)

