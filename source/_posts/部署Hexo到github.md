---
title: 部署Hexo到github
date: 2018-09-24 23:36:50
tags: 琐碎
---

部署Hexo到github


基本的步骤是参考[link](https://mp.weixin.qq.com/s?__biz=MjM5MDEyMDk4Mw==&mid=2650166025&idx=1&sn=50a22c1953f57db0240ca2d1363ba47a&scene=21#wechat_redirect)

**踩过的坑**
> - `hexo d`出现的问题：
   -  `_config.yml`的格式：冒号后面一个空格 ||  除`deploy：`每行开头空两个空格。
   - `Error: spawn git ENOENT`   把git加入到环境变量中解决。
> - 已经配置好`ssh`但是每次部署仍需要输入账号和密码: 未解决QAQ

**选择自己喜欢的主题**
>挑了很久但最终还是决定用大家都说好的Next啦~
链接如下：[link](https://github.com/iissnan/hexo-theme-next)
关于如何自定义可以在`wiki`里看。
 