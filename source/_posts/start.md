---
title: hexo文档
date: 2018-12-11 14:30:34
tags: [hexo,doc,tool]
categories: others
---

现在开始使用hexo 记录代码中不好记录的东西 ...
<!-- more -->
现在开始使用hexo 记录代码中不好记录的东西

## 头部信息

[文章头部信息](https://hexo.io/zh-cn/docs/variables.html#%E9%A1%B5%E9%9D%A2%E5%8F%98%E9%87%8F) 属性和属性值之间必须有一个空格，否则会解析错误 

|    变量    |     描述     |
| :--------: | :----------: |
|   layout   |     布局     |
|   title    |     标题     |
|    date    | 文件建立日期 |
|    tags    |     标签     |
| categories |     分类     |



## 创建新post

```bash
$ hexo new [layout] <title>
```



## 生成并发布

```bash
$ hexo generate --deploy  //生成文章
$ hexo clean  //清除缓存
$ hexo deploy -g  //推送到git 需绑定ssh
$ hexo server  //开启本地端口预览
```