---
title: "[Hexo] 建立BLOG"
date: 2023-02-09 03:58:36
tags:
  - hexo
categories:
  - frontend
cover: https://i.imgur.com/nbsG6QZ.png
feature: true
---

# [Hexo] 建立BLOG

分類: 筆記
新增時間: February 9, 2023 12:14 AM
日期: 2023/02/09
最後編輯時間: February 9, 2023 1:26 AM
狀態: 快速新增
類型: 上課筆記

[1.安装hexo框架_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1hU4y1o7w3?p=2&vd_source=c1365c6bda87bdac707420d133ed93c0)

[](https://aurora.tridiamond.tech/zh/guide/getting-started.html)

### 參考資料

- [https://hexo.io/zh-tw/docs/github-pages](https://hexo.io/zh-tw/docs/github-pages)
- [https://github.com/hexojs/hexo-starter](https://github.com/hexojs/hexo-starter)
- [https://aurora.tridiamond.tech/zh/guide/getting-started.html#依赖环境](https://aurora.tridiamond.tech/zh/guide/getting-started.html#%E4%BE%9D%E8%B5%96%E7%8E%AF%E5%A2%83)
- [https://tridiamond.tech/](https://tridiamond.tech/)
- [https://github.com/auroral-ui/hexo-theme-aurora/tree/main](https://github.com/auroral-ui/hexo-theme-aurora/tree/main)

## 1. 先安裝yarn / nodejs

## 2. 按照下列指令輸入，即可看到下圖畫面(http://localhost:4000/)

```jsx

PS D:\0004_project\Github\pizza-hexo-blog> npm install hexo-cli -g

PS D:\0004_project\Github\pizza-hexo-blog> hexo init blog

PS D:\0004_project\Github\pizza-hexo-blog> cd .\blog\
PS D:\0004_project\Github\pizza-hexo-blog\blog> npm install

PS D:\0004_project\Github\pizza-hexo-blog\blog> hexo s
INFO  Validating config
INFO  Start processing
INFO  Hexo is running at http://localhost:4000/ . Press Ctrl+C to stop.
```

![Untitled](https://i.imgur.com/1aDOvXL.png)

## 3. ****安装主题包****

```jsx
PS D:\0004_project\Github\pizza-hexo-blog\blog> npm install hexo-theme-aurora --save
```

## 4. ****生成主题配置****

```jsx
cp -rf ./node_modules/hexo-theme-aurora/_config.yml ./_config.aurora.yml
```

## 5. 设置permalink(/_config.yml)

```bash
# 修改 permalink 参数为 /post/:title.html
# URL
## Set your site url here. For example, if you use GitHub Page, set url as 'https://username.github.io/project'
url: https://tridiamond.tech
permalink: /post/:title.html
permalink_defaults:
pretty_urls:
  trailing_index: true # Set to false to remove trailing 'index.html' from permalinks
  trailing_html: true # Set to false to remove trailing '.html' from permalinks
```

## 6. ****设置代码高亮****(/_config.yml)

- 把 `highlight` 的启用改为`false`
- 把 `prismjs` 的启用改为`true`
- 把 `prismjs` 下的 `preprocess` 改为 `false`

```bash
highlight:
  enable: false
  line_number: true
  auto_detect: false
  tab_replace: ''
  wrap: true
  hljs: false
prismjs:
  enable: true
  preprocess: true
  line_number: true
  tab_replace: ''
```

## 7.创建 “关于 (about)” 页面

```bash
hexo create page about
```

执行完毕后，你会发现在 `source/` 文件中多处了一个新的文件夹：

```bash
.
└── source
    └── about
        └── index.md
```

## 8. 主題換成aurora(_config.yml)

```bash
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
## theme: landscape
theme: aurora
```

## 9. ****重新生成与本地服务器****

```bash
hexo clean
hexo g
hexo server
```

## 10. 推上github pages

參照裡面的做

[在 GitHub Pages 上部署 Hexo](https://hexo.io/zh-tw/docs/github-pages)

- 注意 : workflow權限記得打開([https://blog.csdn.net/weixin_42282187/article/details/124766382](https://blog.csdn.net/weixin_42282187/article/details/124766382))

![Untitled](https://i.imgur.com/AtAksT9.png)

- 注意 : 一定要建立名為 ***username*.github.io**的儲存庫

[https://cabie8399.github.io/](https://cabie8399.github.io/)

成功了

![Untitled](https://i.imgur.com/nbsG6QZ.png)