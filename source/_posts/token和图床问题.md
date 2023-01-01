---
title: token和图床问题
date: 2023-01-01 15:36:22
tags:建站相关
---





好久没动这个博客了，开了学就放了，最近朋友想用blog传传笔记才又开始动了它



先说说这次重开遇到的问题吧

1. 之前的**图床**不能用了，现在的图床在github上存的，用[PicGo](https://zhuanlan.zhihu.com/p/489236769) 进行图片上传，挺方便的，顺便解决了typora 写笔记时图片总是保存在本地，一来占内存，二来无法在云端享受同样的体验，在Typora的偏好设置中改了改，现在默认将粘贴过来的图片上传到图床。

   1. **图床加速方面**，github访问速度慢，网上有人用Netlify加速，我嫌麻烦，（也是蠢，不想试），就用jsDelivr 加速了，改改PicGo 在github 设置中的自定义域名就OK，原理是上传还是在github上，下载就是通过jsDelivr 加速通道下载了，

      对了图床还有插件功能，以后有时间可以试试

   2. 哦，对，这回搞得时候又把github的**token**原理忘了，刚好之前的token过期了，就用从头搞了一边

      1. token 权限方面一般只有repo管理就行，就既能上传文件，又能下载文件了

      2. token 在本地使用的时候 输入是在密码那里输滴，当然也可以在连接中就直接写入token，当然这样比较麻烦，每回都要复制token，要么，可以通过修改连接的方式直接连接token

         ![连接格式](https://cdn.jsdelivr.net/gh/GuoShuaiGO/Image_Shack_BLOG@main/img/image-20230101112039001.png)

         [修改链接的blog](https://blog.csdn.net/u014090429/article/details/126509415?spm=1001.2101.3001.6650.2&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-2-126509415-blog-126808354.pc_relevant_recovery_v2&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-2-126509415-blog-126808354.pc_relevant_recovery_v2&utm_relevant_index=2)

      3. 还有就是gh工具，不过这个blog的好像不好用，之后再探索探索吧

         [github的token使用方法_chengwenyang的博客-CSDN博客_github token](https://blog.csdn.net/chengwenyang/article/details/120060010)

      4. 当然这样有他不方便的地方，之后每回写笔记要开梯子了，很麻烦

   3. 找图床的时候找到几个比较厉害的图片搜集网站

      [精选 8 个高清二次元动漫壁纸网站推荐 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/354656727)

2. 第二个就是**Hexo 遇到的问题**，我忘了Hexo咋用了，不过还好`hexo --help`能看懂，刚开始hexo命令没法用，之后重新安装了一边之后才能用成，不知道为什么

   1. 这里有一个点就是每回新开hexo的时候都要在文件夹里`npm install` 配置一遍

      [个人博客搭建教程 | 爱扑bug的熊 (cuijiacai.com)](https://blog.cuijiacai.com/blog-building/)

   2. 对了，我现在`hexo serve`  不知道为什么4000端口不能用了，现在要`hexo serve -p 5000` 用5000端口了

      查了一遍发现也没被占用，之后才知道可能是因为我更新了window的原因还是我开了hyper-V的原因，4000端口被保留了

      ![image-20230101114131179](https://cdn.jsdelivr.net/gh/GuoShuaiGO/Image_Shack_BLOG@main/img/image-20230101114131179.png)

​			[原因](https://blog.csdn.net/m0_47696151/article/details/117785566?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-117785566-blog-109691064.pc_relevant_recovery_v2&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-117785566-blog-109691064.pc_relevant_recovery_v2&utm_relevant_index=1)





哦，对了，还发现了**网络报错**，[解决方法](https://blog.csdn.net/u011779517/article/details/122798450)
