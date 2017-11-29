# My work

## 2. 参考了https://github.com/litaotao/litaotao.github.io


## 3. 深度阅读之目录文件说明

```

    
    ### 404 页面，你可以自定义
    ├── 404.html
    ├── README.md
    ### 博客配置文件，基本上是最重要的一个文件之一了
    ├── _config.yml
    ### 博客页面模版目录
    ├── _layouts
    │   ├── default.html
    │   ├── home.html
    │   ├── page.html
    │   └── post.html
    ### 博客文章目录，下面可以按文件夹进行博文分类
    ### 注意，博文文件格式必须是：时间-博文标题.md，参考下面的格式
    ├── _posts
    │   ├── books
    │   │   └── 2017-11-28-books-hadoop.md
    │   └── work
    │       └── 2017-11-28-spark.md
    ### 这个是你的站点地图了，用户可以访问这个文件夹下面的所有文件



## 4. 总结

总的来说，利用 github 搭建博客的步骤为：

- 创建一个 github用户名 + '.github.io' 的新 repo，并克隆到本地
- 把模版，除去 '.git' 的所有文件 copy 到你的repo 中
- 更改 '_config.yml' 配置文件
- 本地试运行，上传到github

