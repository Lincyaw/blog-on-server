---
title: Codespace test
date: 2020-09-20 11:25:37
tags:
---
It's a test post in CodeSpace.

CodeSpace is a virtual environment in cloud, which means I will not have to write blog on my own computer.

[百度](https://www.baidu.com/)

要注意的是vscode里面的图片显示路径要比实际的多一个"..", 我怀疑是github有问题.

这样在vscode中是显示不了的```![图片的测试](/images/headpic.jpg)```

![图片的测试](/images/headpic.jpg)

![东方闪电](/images/headpic.jpg)

这样在vscode能显示,但是实际页面是显示不了的```![图片的测试](../images/headpic.jpg)```

![图片的测试](../images/headpic.jpg)



除了最开始的时候加载有点慢之外, 其他的体验基本都和本地一致, 并且可以随时随地写,真好。

----------------

2020年10月2日10:49:59

今天打算搞个腾讯云的服务器, 托管到腾讯云上(github page)国内访问确实好慢。

目前按照[腾讯云的教程](https://cloud.tencent.com/developer/article/1671013) [静态网站部署](https://cloud.tencent.com/document/product/876/40270)正在布置.

`npm install -g @cloudbase/cli`

`tcb login`

生成之后, 进入public/文件夹,输入```tcb hosting:deploy ./ -e EnvId```即可部署.

结果不能自定义域名!!!!难受  

花了1块钱买了一个一年的域名, 本来以为可以直接用了,结果需要备案 。去备案之后发现域名要服务器，这种云开发的服务不能备案，那就相当于这服务没有用，还是得自己买服务器QAQ

血亏，服务器也好贵
`lincyawblog-18ba58`


----------
2020年10月2日20:57:50

上面的那一段是需要在本地操作的, 因为codespace不能Login(我也不知道为啥)

现在测试一下在codespace上编辑, 然后上传到服务器上的效果.



---

2020年10月3日08:31:02

现在测试一下把博客放到子页面的效果