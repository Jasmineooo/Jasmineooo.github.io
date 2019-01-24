---
layout:     post
title:      Q&A Creating a Blog with Jekyll and Github Pages
subtitle:   CNAME & A Conflict? Want more functions?
date:       2019-01-23
author:     Ama
header-img: img/post-bg-solve.jpg
catalog: true
tags:
    - Blog
---

## 前言

耿耿于怀多少年，辗转多个blog平台，也许是平台不合适，亦或是懒癌发作不愿写，至今并未留下超过一只手的博文。

这些天，偶然发现Github Pages可以当作个人blog，参考[博客搭建详细教程](https://github.com/qiubaiying/qiubaiying.github.io/wiki/博客搭建详细教程)后，*在此感谢BY, Huxpro等*，有前人栽树，我的blog：**Ama's Data World**才能诞生，还买了个域名：[**amathlover.com**](amathlover.com)，准备大干一场，希望不是空话。

回想过去，总是想得太多，做得太少，今起，是否要踏踏实实地码字写文呢？且看行动吧。

作为blog开门第一篇，也是2019年第一篇，将建立此blog遇到的问题和解决办法分享如下，希望对朋友们有帮助。




## 1 图床

图床对于markdown写作是非常重要的。

Windows下有MPic代替IPic，但只支持七牛。

七牛临时域名有30天有效期，之后需用自己的域名，且需备案，备案要买虚拟主机，像我一样不想折腾这些的小伙伴们，我们还有办法。

### 直接拖进Typora中

话说Markdown编辑器Typora中，咱可以直接将图片拖进来，并自动生成链接，但图片要一起放进站点文件夹中，据说Github里放太多静态文件会被批的，咱们还是找图床吧。

### 免费图床

据说 [极简图床](https://jiantuku.com/)、[sm.ms](https://sm.ms/)、微博图床chrome插件 等很好用，图片会上传到微博相册中，可惜了，这些天，前两个打不开，网页显示“升级维护中”，插件总装不上。

只好先用最笨的方法，手动上传到微博图床中。

### 笨办法

1. 注册微博小号

2. 打开[微相册](http://photo.weibo.com/6969080201) 

3. 准备好一篇文章需要的所有图片

4. 用FileOptimizer压缩一下

5. 上传图片

6. 获取外链：点击图片-查看大图-右键图片复制图片链接

7. 写入`.md`文件中 

   

## 2 `CHAME` 与 `MX` 冲突

用阿里云解析买好的域名时，按照教程所说，添加`A`或`CHAME`记录时，出现blog网页打不开，或出现：请求失败 “CHAME”记录与“MX”记录冲突。因为同时已经自带解析了阿里云赠送的企业邮箱，怎么办呢？网上搜索后发现很多人也有这些问题，且没得到很好解决。

仔细阅读Github帮助文档（[Using a custom domain with Github Pages](https://help.github.com/articles/using-a-custom-domain-with-github-pages/)）后，解决方案如下：

1. [设置一个顶端域名](https://help.github.com/articles/setting-up-an-apex-domain/)，如`example.com`：在DNS服务商添加`A`记录@，指向如下IP地址：
```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

2. [设置一个子域名](https://help.github.com/articles/setting-up-a-www-subdomain/)，如`www.example.com`：在DNS服务商添加`CHAME`记录`www`，指向`username.github.io`，其中`username`为你的Github名。

3. 等待一会儿，可能睡一觉起来就好了。


<div style='display: none'>
![published](http://wx3.sinaimg.cn/mw690/007BDy7nly1fzfef1coeqj30ej06bwen.jpg)
</div>


## 3 添加社交账号 

BY的博客模板中提供了weibo, zhihu, github, facebook, jianshu, twitter，而我还想加上微信wechat怎么办？No, 不是个人微信号，是我的微信公众号。解决办法如下：

- `_config.yml`中找到 `# SNS settings`，添加`wechat_username: xxxxxxx` 写上公众号的微信号。
- `_layouts`文件夹，`page.html` 中找到
```markdown
  {% if site.github_username %}
  ...
  {% endif %}
```

- 在之后添加：
```markdown
  {% if site.wechat_username %}
  <li>
	<a target="_blank" href="https://weixin.sogou.com/weixin?type=1&s_from=input&query={{ site.wechat_username }}&ie=utf8&_sug_=n&_sug_type_=">
		<span class="fa-stack fa-lg">
			<i class="fa fa-circle fa-stack-2x"></i>
			<i class="fa fa-weixin fa-stack-1x fa-inverse"></i>
		</span>
	</a>
  </li>
  {% endif %}
```

- 图标代码在[Font Awesome](https://fontawesome.com/start)找哦，比如微信，就输入weixin或wechat就可以搜索了。
添加后侧边栏效果如图：
![wechat](http://wx3.sinaimg.cn/mw690/007BDy7ngy1fzgft5413sj301t01udfl.jpg)
这样点开后，会到搜狗微信公众号搜索的网页，算是解决了。

- 同理，在`_includes`文件夹中`footer.html`类似位置也添加类似代码，这样，网页底部也有了。如果想添加其他的，再去上面图标网站找。



## 4 添加访问量

先在head里面添加这句：
```markdown
<script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>
```

再在`_includes`文件夹中`footer.html`找到`copyright`部分，如果和我一样是小白，点赞数为零，让我们大胆地注释掉关于Github点赞数的`<iframe>`部分吧。

添加访问量显示代码如下：

```markdown
<!-- 访客数 -->
<i class="fa fa-user"></i>
<span id="busuanzi_container_site_uv">
	<span id="busuanzi_value_site_uv"></span>
</span>

<!-- 总浏览量 -->
<i class="fa fa-eye"></i>
<span id="busuanzi_container_site_pv">
	<span id="busuanzi_value_site_pv"></span>
</span>
```

效果如图：

![count](http://wx3.sinaimg.cn/mw690/007BDy7ngy1fzgft97nfrj30a202bwef.jpg)

呀 暴露了只有我一个访客呢~




## 5 Windows环境本地调试

Windows环境下，请参考[解决办法by Caiyun](https://agcaiyun.cn/2017/09/10/personalBlog/)

对应英文参考资料：[Run Jekyll on Windows](http://jekyll-windows.juthilo.com/1-ruby-and-devkit/)

我在安装过程中遇到的问题也一并写入以下简要步骤里：

- Get Ruby for Windows，安装 Ruby 2.3 及以上，起初我按Caiyun说的装了2.2，安装到后面出现Jekyll仅适用于至少Ruby 2.3版本，只好重装2.3，之后挺顺利的。

- 按英文资料安装Ruby

- Get the Ruby DevKit，按照说明Extract

- 依次运行以下命令
    ```markdown
    <!-- 我装在了D盘里，所以这里是D:\ -->
    cd D:\RubyDevKit
    ruby dk.rb init
    ruby dk.rb install 
    ```

- install Jekyll Gem，执行：
  ```markdown
  gem install jekyll
  ```

- install jekyll bundler，执行：
  ```markdown
  gem install jekyll bundler
  ```

- 进入blog所在文件夹，执行：
  ```markdown
  jekyll s
  ```
  或
  ```markdown
  jekyll serve
  ```
  这两个是一个意思

- 如果没有问题，就可以去[http://127.0.0.1:4000/](http://127.0.0.1:4000/) 本地预览blog啦。

- 可是，我的显示出错 Deprecation: The 'gems' configuration option has been renamed to 'plugins'. Please update your config file accordingly.

- 于是，找到配置文件`_config.yml`，将 `gems: [jekyll-paginate]`中的`gems`改为 `plugins`

- 执行命令
  ```markdown
  cd D:\RubyDevKit
  gem install jekyll-paginate
  ```

- 回到blog所在文件夹，执行：
  ```markdown
  jekyll s
  ```
  这下没问题了，调试之后按`Control+C`停止serve。

  

## 结语

还有一些问题没有解决，比如百度和google收录，没有备案的网站是不是不好被快速收录呢？等等看吧~

工具都是次要的，不要因为建站而忘记自己当初想做什么，嗯，想学data science，那就学起来吧！



## 更多资料
32个炫酷配置：[hexo的next主题个性化教程：打造炫酷网站](https://blog.csdn.net/qq_33699981/article/details/72716951)

> 虽然是关于Hexo的，但并不妨碍我们借鉴过来。
