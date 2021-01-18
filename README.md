# hexo-generator-readme
[![NPM version](https://badge.fury.io/js/hexo-generator-index.svg)](https://www.npmjs.com/package/hexo-generator-readme)

##### [中文](./README_CN.md)

auto generator readme file for hexo blog

It generator a readme file thant you can store it in your git repository.

### features

* custom readme template
* categories filter able
* categories custom sort
* post sort
* post filter in readme

### Installation

```shell
npm i hexo-generator-readme -S
```

### Oportions

Add or modify the following sections to you root _config.yml file:

```yaml
generator-readme:
  categories:
    name: 1
  order_by: ''
  layout: ''
```

* **categories**: Which categories you will use for generation, the number behind it is used for sorting, the smaller the number, the higher the sorting
    * default: all the categories will be generated in the readme
    
* **order_by** Post order
    * default: date descending
    
* **layout** the layout template name.you should put this file in you theme layout folder; eg: `node_modules/hexo-theme-next/layout/readme.njk`
    * default: 'readme'
    
*** Usage

The `skipInReadme` parameter in ths post [Front-matter](https://hexo.io/docs/front-matter) will be used to filter this post generated in the readme file;

```yaml
---
title: Hello World
date: 2021/1/17 20:46:25
skipInReadme: true
---
```

You should create a readme template into the theme layout file. in the template ,you can use the formatted `page.categories` variable; and all other `locals` variable you can use.
[more about](https://hexo.io/api/locals)

eg: a readme template like this :

```template
{%- for c in page.categories %}
## {{c.name}}
{%- for p in c.posts %}
#### [{{ moment(p.date).format('YYYY-MM-DD') }}] [{{p.title}}](https://blog.linxiaodong.com/{{p.path}})
{%- endfor %}
{%- endfor %}
```

this will build a `README.md` like [github.com/buxuku/buxuku.github.io](https://github.com/buxuku/buxuku.github.io)

## License

MIT