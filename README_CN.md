# hexo博客系统生成Readme文件插件

[![NPM version](https://badge.fury.io/js/hexo-generator-readme.svg)](https://www.npmjs.com/package/hexo-generator-readme)

自动为hexo博客生成一个readme文件,你可以方便地把它放在仓库里面用来做展示.

### 特性

* 自定义模板
* 可以过滤掉不想展示的分类
* 分类可以进行自定义排序
* 文章可以进行排序
* 文章可以自定义过滤掉不在readme文件中展示

### 安装

```shell
npm i hexo-generator-readme -S
```

### 配置

在根目录下面的_config.yml文件中添加或者修改以下配置

```yaml
generator_readme:
  categories:
    name: 1
  order_by: ''
  layout: ''
```

* **categories**: 你将用来展示的分类,后面的数字可以用来进行排序的,数字越小,将越排在前面.
    * 默认: 如果不配置该项,将展示所有的分类,但不支持自定义排序的实现 

* **order_by** 文章排序
    * 默认: 文件里面的data属性

* **layout** 用来渲染的布局模板名称 eg: `node_modules/hexo-theme-next/layout/readme.njk`
    * 默认: 'readme'

*** 使用

可以在文章的 [Front-matter](https://hexo.io/docs/front-matter) 设置`skipInReadme`属性,用来过滤掉不想在readme中展示的文章 

```yaml
---
title: Hello World
date: 2021/1/17 20:46:25
skipInReadme: true
---
```

你需要创建一个模板文件放在主题的`layout`目录里面.在这个模板文件里面,你可以使用`page.categories`这个变量,它是一个已经处理好了的变量.同时你也可以使用所有的`locals`变量
[查看更多](https://hexo.io/api/locals)

比如,一个readme模板可以大概长成这个样子 :

```template
{%- for c in page.categories %}
## {{c.name}}
{%- for p in c.posts %}
#### [{{ moment(p.date).format('YYYY-MM-DD') }}] [{{p.title}}](https://blog.linxiaodong.com/{{p.path}})
{%- endfor %}
{%- endfor %}
```

这将生成一个 `README.md` 文件, 可以参看 [github.com/buxuku/buxuku.github.io](https://github.com/buxuku/buxuku.github.io)

## License

MIT
