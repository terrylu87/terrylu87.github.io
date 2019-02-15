---
excerpt: 记录使用过程中遇到过的坑和自己的一些思考
layout: post
category : blog
tags: [jekyll, blog, chinese, multilingual, font, github-page]
lang: zh
---

原文地址：https://terrylu87.github.io/blog/2019/02/15/使用-markdown-在-github-page上写博客 <br>
转载请注明出处
## 1 使用Markdown+jekyll在github page上写博客

### 1.1 在本地测试
#### 1.1.1 如果局域网无法访问
想用手机测试移动端的排版质量，结果访问被拒绝,如下图：

<img src="https://github.com/terrylu87/terrylu87.github.io/blob/master/images/2019-2-15/visit_lan_fail.png?raw=true" width="49%">

把 \<username\> 换成自己的 github 帐号，运行以下命令：<br>

```bash
  $ git clone https://github.com/<uername>/<username>.github.io.git blog
  $ cd blog
  $ jekyll serve --host=0.0.0.0
```

参数 --host=0.0.0.0 是为了在局域网内访问测试博客，这样就可以用手机测试移动端的排版质量。不加这句的话只能用本机访问 http://127.0.0.1:4000 来访问，别的ip过来的请求会被拒绝。


#### 1.1.2 如果遇到Theme无法正常显示时
本地测试需要打开 \_config.yml 中的注释，设置 ASSET_PATH，**注意此修改仅限本地测试用，不要上传到 github page 上**

```bash
# ASSET_PATH : false
# uncomment this line to make theme work in local network
  ASSET_PATH : /assets/themes/hooligan/
```

#### 1.1.3 如果 code block 无法正常渲染
如图：
<img src="https://github.com/terrylu87/terrylu87.github.io/blob/master/images/2019-2-15/code_render_fail.png?raw=true" width="100%">
```bash
# 安装 redcarpet
$ sudo gem install redcarpet
$ cd blog
# 使用 redcarpet 解析 markdown
$ cat "markdown: redcarpet" >> _config.yml
# 重启 jekyll
$ jekyll serve --host=0.0.0.0
```
之后显示正常：
<img src="https://github.com/terrylu87/terrylu87.github.io/blob/master/images/2019-2-15/code_render_right.png?raw=true" width="100%">

#### 1.1.4 中文显示
如果中文显示乱码，就需要在文件头部加上 `lang: zh` 。下面是此篇博客完整的 Header Section<br>
```
---
excerpt: 记录使用过程中遇到过的坑和自己的一些思考
layout: post
category : blog
tags: [jekyll, blog, chinese, multilingual, font, github-page]
lang: zh
---
```


### 1.2 图片资源管理

#### 1.2.1 图片引用方式的选择
在 markdown 中显示图片主要有3种方式：

1 直接链接,此方法优点是简单。

```
![](https://github.com/favicon.ico)
```
![](https://github.com/favicon.ico)

2 引用链接，此方法可以复用链接的定义，但是由于不能像变量那样自由引用，所以适用场景非常有限。

```
[github_img]:https://github.com/favicon.ico
![][github_img]
```
[github_img]:https://github.com/favicon.ico
![][github_img]

3 使用 HTML 格式的block，这是我尝试下来唯一能成功修改图片大小的方法。width的百分比是屏幕宽度，也可以用像素设置。

```
<img src="https://github.com/favicon.ico" width="10%" title="Github Logo">
```
<img src="https://github.com/favicon.ico" width="10%" title="Github Logo">

#### 1.2.2 图片资源的存储
考虑到在编辑并发布在github.io上之后，需要将文章转发到CSDN或其他博客平台上。所以图片引用不能采用相对链接的方式。那么需要一个平台来存储图片。网上有 markdown 编辑工具集成了云服务，如 [markdownmonster](https://markdownmonster.west-wind.com/) ，并且可以拖拽操作，十分方便。缺点是多了云服务平台这个依赖项，以及只有windows版本。<br>
最后我决定将图片存在 github page 项目中，引用时直接调用 github 的链接。虽然编辑和管理起来稍麻烦一些，但是文章写完之后可以随意复制粘帖到各个支持 markdown 的平台，不会有死链接。想要直接引用 github 项目中的图片，需要得到图片的raw地址，在链接后面加上`?raw=true`<br>
例如链接 https://github.com/terrylu87/terrylu87.github.io/blob/master/images/2019-2-15/visit_lan_fail.png 其实是一个网页，只有 https://github.com/terrylu87/terrylu87.github.io/blob/master/images/2019-2-15/code_render_right.png?raw=true 才是真正的图片地址。<br>
希望能发现有更好的工具，或者更好的方法，可以直接利用github的空间来存储和管理图片。

## 2 发布到别的博客平台
github page 的流量较少，可以考虑将博客发布到别的平台加强交流。所以只考虑使用最基本的markdown语法，结合上文对图片采取的绝对地址引用，编辑完成后复制粘贴到平台的 markdown 编辑器中就可以直接发布了。实测 CSDN 可以无缝对接，Header Section 需要删掉。
