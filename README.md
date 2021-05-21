# Github Page
使用主题: [Next](https://github.com/theme-next/hexo-theme-next)

主页链接: [Wateramelon](https://Lincyaw.github.io)

网站地址: [Lincyaw](www.lincyaw.xyz)



---

## 配置方式

本来是Codespace+Github Page组合的, 这样可以完全在线上写, 不依赖任何本地的环境，但是这样的问题是国内访问速度太慢。

然后到国内服务器托管，但是自定义域名还需要购买服务器？

然后又自己买了服务器，想着光拿这个服务器写个博客也太可惜了，就自己在服务器上又搭建了一遍。结果在Codespace上传国内服务器的时候，速度又慢的可怜...唉，两者不可兼得，万恶的墙。



安装必要环境: 

```shell
sudo apt-get install git

sudo apt-get install npm # 安装npm
sudo npm i -g npm # 升级到最新版本

sudo npm i -g n   # 安装node.js的版本管理工具
# sudo n latest  # 安装最新版本
sudo n stable  # 安装稳定版

npm install -g hexo-cli  # 安装hexo
npm install hexo-deployer-git --save # 安装deployer工具


wget https://github.com/jgm/pandoc/releases/download/2.10.1/pandoc-2.10.1-1-amd64.deb   # linux中下载pandoc , win中自行下载
sudo dpkg -i pandoc-2.10.1-1-amd64.deb
npm uninstall hexo-renderer-marked --save   # 自带的公式渲染不太好
npm install hexo-renderer-pandoc --save    # 用pandoc
```

上传三板斧

```sh
hexo clean && hexo g -d   // 清除已有文件+生成+部署
```

---

自己安装的[参考文章](https://zhuanlan.zhihu.com/p/120743882)

在装好之后发现别人用[宝塔面板](https://cloud.tencent.com/developer/article/1662792)做的也太轻松了吧, 我搞那个hook搞了半天QAQ. 但是必须要centos用

