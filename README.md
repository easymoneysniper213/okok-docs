# 讲解文档

文档主要死在master上，把项目拉下来之后可以 

`mkdocs serve`
  
命令在本地运行，页面逻辑跟前端的pages差不多，语言是用的 markdown。

我现在还没完全搞明白怎么publish的，但应该是在完成后先 pull 一下 master，再执行 

`mkdocs gh-deploy --clean `
  
命令，就会直接部署到 github pages 的网站，也就是 
 
`https://easymoneysniper213.github.io/okok-docs/`
  
执行完 gh-deploy 后得记得把改动再推到master。

主要注意的是 gh-pages 的分支是个静态分支，改上面的内容没有任何用户，下一次执行 gh-deploy 会直接覆盖
