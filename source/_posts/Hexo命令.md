---
title: Hexo命令
date: 2022-03-13 17:37:37
update: 2022-11-07 12:14:14
swiper: true # 将改文章放入轮播图中
swiperImg: '/medias/2.jpg' # 该文章在轮播图中的图片，可以是本地目录下图片也可以是http://xxx图片
swiperDesc: 'Hexo命令' #文字描述
top: true
categories: 'hexo' #分类
tags: 配置
---

## hexo

### 启动本地服务

```markdown
hexo s
```

### 创建文章

```markdown
hexo new "此处输入文章名字"
hexo new page "页面"
```

### 编写文章

```markdown
title: Hexo 命令 #本文标题
date: 2022-01-13 17:37:37 #创建时间
update：2022-01-13 18:00:00 #更新日期
comments: true #是否可评论
layout: post # 公开文章
toc: true #是否显示文章目录
swiper: true # 将改文章放入轮播图中
swiperImg: '/medias/2.jpg' # 该文章在轮播图中的图片，可以是本地目录下图片也可以是 http://xxx 图片
swiperDesc: 'Hexo 命令' #文字描述
top: true #文章是否顶置
onlyTitle: true #是否显示时间/字数统计/时长/阅读量信息
categories: "hexo" #分类
tags: 配置 #标签
```

### 发布文章

```markdown
// 也可以写成一条命令 hexo clean && hexo g && hexo s
hexo clean 清除缓存
hexo g 生成静态文件
hexo d 网站部署
hexo s 启动服务器
```

### hexo 创建

```js
npm install hexo-cli -g
hexo init blog （blog 项目名）
cd blog
npm install
hexo server
```

### Typora 快捷键

```markdown
Ctrl+1：一级标题
Ctrl+2：二级标题
Ctrl+3：三级标题
Ctrl+4：四级标题
Ctrl+5：五级标题
Ctrl+6 ：六级标题
Ctrl+0：段落

Ctrl+I：斜体
Ctrl+B：粗体
Ctrl+U：下划线
Alt+Shift+5：删除线
Ctrl+Shift+Q: 文字引用

方法一：[链接文字](链接地址 '链接描述')
例如：[示例链接](https://www.example.com/ '示例链接')

方法二：<链接地址>
例如：<https://www.example.com/>

{% asset_img 图片路径 图片描述 %}
post_asset_folder: true
{% asset_img example.jpg This is an example image %}
```

### Front-matter 预定义参数

```markdown
配置选项 默认值 描述
title Markdown 的文件标题 文章标题，强烈建议填写此选项

date 文件创建时的日期时间 发布时间，强烈建议填写此选项，且最好保证全局唯一

swiper false 表示该文章是否需要加入到首页轮播封面中

swiperImg 无 表示该文章在首页轮播封面需要显示的图片路径，如果没有，
则默认使用文章的特色图片

swiperDesc 无 表示该文章在首页轮播封面需要显示的文字描述（摘要），
如果没有，则使用 excerpt，如果 excerpt 也没有，则取文章内容

img 无 文章特征图，该文章显示的图片，没有则默认使用文章的特色图片

excerpt 无 文章描述（摘要），该文章在首页的描述文字，如果没有，
则取 swiperDesc,如果 swiperDesc 也没有，则取文章内容（优先取<!-- more -->上面的内容）

top false 将该值设为 true，则将该篇文章显示在首页的置顶栏目中

toc true 将该值设为 false，则该篇文章不显示右侧目录

tocOpen true 将该值设为 false，则该篇文章右侧目录默认收缩

onlyTitle false 文章详情页头部是否只显示标题，不显示日期等信息

comments true 将该值设为 false，则该篇文章不显示评论

share true 将该值设为 false，则该篇文章不显示分享按钮

copyright true 将该值设为 false，则该篇文章不显示版权声明

donate true 将该值设为 false，则该篇文章不显示打赏按钮

bgImg - 单独为这篇文章设置背景图片或者背景颜色，可以是数组，
数组里面放图片链接，可以是字符串，字符串里面是颜色值，空值则背景颜色透明

bgImgTransition fade 该篇文章的 bgImg 设置为数组,该值表示背景图片切换的动画,
有三种值（fade, scale, translate-fade）

bgImgDelay 180000(三分钟) 该篇文章的 bgImg 设置为数组,
该值表示背景图片切换的延迟时间,

categories 无 文章分类，本主题的分类表示宏观上大的分类，
只建议一篇文章一个分类

prismjs 无 如果使用的是 hexo 自带的 prismjs 代码高亮，通过设置该值为该篇文章
设置不同的代码高亮主题（default, coy, dark, funky, okaidia, solarizedlight, tomorrow, twilight）

tags 无 文章标签，一篇文章可以多个标签

mathjax false mathjax 公式

imgTop true 设置为 false 则文章和自定义页面顶部不要图片
```

### 参考链接

<https://blog.csdn.net/wsmrzx/article/details/81478945>
<https://yuang01.gitee.io/post/hexo-theme-bamboo/front-matter/>
