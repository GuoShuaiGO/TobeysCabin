---
title: Git编码GBK与UTF-8的bug解决
categories:
  - [配置问题]
tags:
  - Git
date: 2023-10-22 18:04:49
---

好久没有写blog了，最经遇到了一个绷不住了的bug，写一下解决过程

<!-- more-->



出错：

在Git Bash中执行`conda activate xxx`的时候报错

![image-20231022173726535](https://cdn.jsdelivr.net/gh/GuoShuaiGO/Image_Shack_BLOG@main/img/image-20231022173726535.png)

先上网查了有没有人出现过相关情况，结果也是没有。

不过也确实查到比较好的建议

```bash
source activate
```

该命令能够有效的开启conda环境

还学到一个初始化conda命令，但是感觉着实没有用处`conda init`也写着吧说不定啥时候有用捏



就自己看报错吧

> File "D:\software\miniconda\lib\site-packages\conda\activate.py", line 1222, in main
>      print(activator.execute(), end='')
>  UnicodeEncodeError: 'gbk' codec can't encode character '\xbb' in position 1851: illegal multibyte sequence

一眼望过去是编码格式有问题，但是出问题的文件在conda本身自带的python文件呀。又不敢改。担心改出某个问题，当时没发现，之后再用conda的时候一处错。还忘了这个地方改过就寄



就不断尝试，后来发现在pycharm中的Terminal命令框执行conda命令和直接在Git-bash中效果不一样

![image-20231022174412476](https://cdn.jsdelivr.net/gh/GuoShuaiGO/Image_Shack_BLOG@main/img/image-20231022174412476.png)



直接source activate激活conda就可以，甚至直接换一下命令，`source activate xxx`也就可以。

![image-20231022174605247](https://cdn.jsdelivr.net/gh/GuoShuaiGO/Image_Shack_BLOG@main/img/image-20231022174605247.png)



**这里其实我也在pycharm中也报过想bash中的错误，忘了怎么爆出来的了，复现不了了**





然后我就纳闷了，刚开始以为是因为pycharm中用的是`/bin/sh.exe` 和直接的Git-bash不一样，上网搜了一下，按理来说前者是后者阉割版。按理来说应该一样。然后就尝试没在pycharm上打开sh.exe。直接点击打开了，结果和Git-bash报的错一样。我就算切换到项目所在的目录执行sh.exe的conda相关命令也一样【我甚至还尝试bash.exe，也是同样的报错】



OK了，能猜个八九不离十，应该就是编码错误。不是啥配置问题。通过前面检索查问题也上网大概了解到Win用的是GBK编码，然后python用的是UTF-8二者编码不一致。估计是这里出的问题。然后pycharm的sh.exe 调用应该是修改了哪里的默认编码，导致能够识别UTF-8了，不用GBK了皆大欢喜了。



解决方法：

就是把那个文件`D:\software\miniconda\Lib\site-packages\conda\activate.py`中的这一行的编码提前处理一下，你不是gbk编码UTF-8的字符出问题嘛，就提前编码上一下，把错的去掉`ignore`，然后再解码。你再自己编码吧，一定不会出问题了

```python
print(activator.execute().encode('gbk', 'ignore').decode('gbk'), end='')
```



这是暴力解决方法。然后我也想找巧方法，让直接打开的GIT-bash窗口能够像pycharm一样处理UTF-8的文本。可惜了没解决。参考了下面这个blog，相关配置【包括环境变量我都没改回去，看吧说不定在其他地方有用捏，如果后面因为这个原因出错的话就参考这个blog[Git bash 编码格式配置_02_git bash 编码-CSDN博客](https://blog.csdn.net/weixin_40816738/article/details/108433309)改回去】，那个config的global修改修改的是`C:\Users\guo\.gitconfig`配置文件，export命令的修改重启一下Terminal就没有了，也不用担心，环境变量到时候删了就行



虽然知道咋改了，最后还是没狠下心来改conda的库文件😥，看吧说不定人家还有用捏。反正我现在在pycharm里面也能用conda+Git

如果改了的话解决的效果图如下

解决效果图：

![image-20231022173104053](https://cdn.jsdelivr.net/gh/GuoShuaiGO/Image_Shack_BLOG@main/img/image-20231022173104053.png)
