# 讲解文档

### 前提
可以把文档当作一个小项目，把这个项目的东西先用 `git clone` 复制到本地，然后就可以对文档的内容进行操作。

### 安装 
需要安装 mkdocs 和页面样式:

    pip install mkdocs
    pip install mkdocs-material

lsn 遇到了 `pip install` 会直接报错，可以找他debug，好像是跟开了代理有关。

### 主要操作
文档主要是在master上，把项目拉下来之后可以 

    mkdocs serve
  
命令在本地运行，页面逻辑跟前端的pages差不多，语言是用的 markdown。

我现在还没完全搞明白怎么publish的，但应该是在完成后先 pull 一下 master，再执行 

    mkdocs gh-deploy --clean
  
命令，就会直接部署到 github pages 的网站，也就是 
 
    https://easymoneysniper213.github.io/okok-docs/
  
执行完 gh-deploy 后得记得把改动再推到master。

### 链接问题
github真的是链接很难受，搞了半天老是卡，也没搞明白怎么弄代理， 反正如果说连接不到 github repo， 可以先用

    git ls-remote https://github.com/easymoneysniper213/okok-docs.git/

看链接行不行。我有几次调用这个命令都用不了。这个时候用不了可以考虑清空 DNS 缓存，

Windows 是用：

    ipconfig/flushdns

苹果 是用：

    sudo dscacheutil -flushcache; sudo killall -HUP mDNSResponder

然后重新把项目 git clone 下来。这种方法有点愚蠢，但我弄了半天好像也只能这样，有别的解决方法你们分享一下。

### 注意事项
- gh-pages 的分支是个静态分支，改上面的内容没有任何用户，下一次执行 `gh-deploy` 会直接覆盖