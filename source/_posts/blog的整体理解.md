---
title: blog的整体理解
date: 2023-01-05 22:58:46
categories: site
tags: 	
     - GitHub page
     - netfily 两种功能实现
     - hexo 原理
---





# blog的整体理念

涉及

- `github page`的使用
- `Hexo` 的原理
- `netlify` 的两种使用方法



<!-- more-->



## Hexo原理

先讲讲Hexo使用原理吧



#### 首先  [Hexo](https://hexo.io/zh-cn/) 是一个博客框架

```bash
.
├── node_modules：#依赖包-安装插件及所需nodejs模块。
├── public  #最终网页信息。即存放被解析markdown、html文件。
├── scaffolds #模板文件夹。即当您新建文章时，根据 scaffold生成文件。
├── source  #资源文件夹。即存放用户资源。
|   └── _posts #博客文章目录。
└── themes #存放主题。Hexo根据主题生成静态页面。
├── _config.yml   #网站的配置信息。标题、网站名称等。
├── db.json：#source解析所得到的缓存文件。
├── package.json  # 应用程序信息。即配置Hexo运行需要js包。
```

##### 粗俗的解释原理：

blog的本质就是markdown文档和相对应的管理，所以Hexo将blog的这两个功能分离为数据（就是你要编写的markdown文档 存放在`source`文件夹中）以及框架管理`themes` `scaffolds` 文件夹中的东西，其中scaffolds存放的是`layout`的原始信息，方便使用`hexo new post(或者是其他layout) "title"` 创建layout模板，而layout的渲染，和其他好看的评论呀，搜索功能呀，猫咪装饰呀，都在于`themes` 主题中选择的主题而言了，最后

```
hexo clean #删除public文件夹
hexo generate # 将以上数据和框架结合起来，形成对应的html，css，JavaScript等前端静态文件
hexo serve -p 5000#我的是因为4000被空了，所以用5000 端口，来展示public中的内容
hexo deploy #将public部分部署到对应的前端网页
```



##### 涉及代码的解释就是：

呜呜呜，我不懂😭😭😭



反正以我目前的理解来说，首先要理解什么是

###### NodeJS

这是一个JavaScript的开发环境，基于chrome V8引擎，能够使开发者摆脱浏览器的限制，（原本JavaScript 只能在浏览器中运行，导致他只能担任前端脚本的作用，而nodejs让他能够脱离浏览器的限制，在nodejs中运行）



###### npm

node package manager 使nodejs的包管理系统，就像各种语言都有的包一样，npm是能够在nodejs中运行的语言包，hexo就是一个包，但是这个包里面的使用的代码不是纯粹的JavaScript 而是所谓的nodejs模板引擎



###### nodejs 模板引擎

其实就是变形的语言，模板引擎是第三方模块。 **让开发者以更加友好的方式拼接字符串，使项目代码更加清晰、更加易于维护。** 实现原理就是用许多变量来代替JavaScript等语言（主要是JavaScript）中的部分必须要的原本要固定的代码

[nodejs模板引擎有些什么](https://www.php.cn/website-design-ask-484671.html)



所以我的blog所谓的不断改动如果我没用学对应的模板引擎的话，实现更多的功能无非就是用不同的主题，然后进行配置........



坦率地说，这样做的话没有什么技术含量，所以我之后也就不会咱们动我的site了。。。





#### github page

其实很简单，就是仓库名要设置成`<用户名>.github.io` 之后调用setting中的page选项就可以了，一种博客实现方式就是通过`hexo deploy` 将pulic部分部署到上面写的仓库中，之后用github page功能将这些离散的源静态文件（html，css，JavaScript）部署成网页的形式



#### netlify

netlify有两个功能

###### 网站部署

一个是可以它可以实现GitHub page的功能，链接到github的仓库之后当仓库发生更改，Netlify监测到变更时进行拉取并直接伺服（伺服就是实现GitHub page的网页部署功能）。

[个人博客搭建教程 | 爱扑bug的熊 (cuijiacai.com)](https://blog.cuijiacai.com/blog-building/) 这个blog里面就实现了这种功能，比第二个功能需要多设置的就是，部署时，需要在那个云端产生一遍它的pulic文件（应该是我的public和他的public会有差别，导致需要按照他的路径生成一遍public），这也就是需要多设置的这两个地方

![image-20230105224733358](https://cdn.jsdelivr.net/gh/GuoShuaiGO/Image_Shack_BLOG@main/img/image-20230105224733358.png)



![image-20230105224814636](https://cdn.jsdelivr.net/gh/GuoShuaiGO/Image_Shack_BLOG@main/img/image-20230105224814636.png)





要在它那里运行一遍npm 的netlify这个命令，而之前定义的netlify这个命令就是`npm run clean && npm run build` 这两句npm包命令，而这两个命令在之前定义为`hexo clean和hexo generate` 这两条hexo命令，注意，这里关于npm命令的设置，都在

![image-20230105225134254](https://cdn.jsdelivr.net/gh/GuoShuaiGO/Image_Shack_BLOG@main/img/image-20230105225134254.png)

package.json 这个的设置里面，这个文件存放的是npm对hexo这个包的管理配置信息

![image-20230105225330622](https://cdn.jsdelivr.net/gh/GuoShuaiGO/Image_Shack_BLOG@main/img/image-20230105225330622.png)



并且netlify能够自动生成https网站，绑定外面申请的域名，比如说我的 `tobeycabin.love` 挺棒的





###### github加速

由于netlify访问速度比github快，所以可以通过netlify绑定github对应仓库，之后访问netlify就等价于访问对应仓库路径

比如说我的图床就在netlify中加速了一下

https://imgshack.netlify.app/



[QQ图片20230101095724.jpg (1080×1080) (imgshack.netlify.app)   头像链接https://imgshack.netlify.app/img/QQ图片20230101095724.jpg](https://imgshack.netlify.app/img/QQ图片20230101095724.jpg)



对应路径就是github仓库中的路径，之后看吧，如果这样的访问速度快的话我就用它来加速我的图床了
