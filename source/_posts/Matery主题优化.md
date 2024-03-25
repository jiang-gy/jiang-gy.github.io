---
title: Matery主题优化
tags:
- Hexo博客
---

主要参考博客[魔改记录](https://fenghen0918.github.io/2020/10/22/hexo/hexo-bo-ke-you-hua-pian-matery-yi/#toc-heading-1)，大佬博客总结得很详细，但是由于大佬blog是较早之前写的，有些功能仍然有些不适用，在配置过程中踩了一些坑，因此，此处记录一下过程（有用部分直接就cv了），推荐直接访问原博客。
## 1 基本页面功能
此部分也可以参考原本的`read.me`,功能实现基本相似
### 1.1 增加页面

> 增加页面的步骤都基本相同，创建`tags`标签页、`categories`分类页，`about`关于我页、 `contact`留言板页、`friends`友情链接页、均可以使用这个步骤

1. 如果在你的博客 source 目录下还没有，就输入以下命令（站点目录打开的命令行）来新建一个：
   
    ```
    hexo new page "页面的英文"     # 如：hexo new page "tags"
    ```
    
2. 编辑你刚刚新建的页面文件 /source/tags/index.md，至少需要以下内容：
   
    ```
    ---
    title: tags
    date: 2020-06-19 16:23:38
    type: "页面的英文"    # 如：type: "tags"
    layout: "页面的英文" # 如：layout: "tags"
    ---
    ```
    
    > 关于 `contact`留言板页：
    >
    > 留言板功能依赖于第三方评论系统，激活评论系统才有效果，下面会有介绍
    >
    > 关于`friends`友情链接页：
    >
    > 如果你想增加内容，在你的博客 source 目录下新建 `_data` 目录，在 `_data` 目录中新建 `friends.json` 文件，输入以下内容：
    
    ```
    [{
        "avatar": "http://image.luokangyuan.com/1_qq_27922023.jpg",
        "name": "码酱",
        "introduction": "我不是大佬，只是在追寻大佬的脚步",
        "url": "http://luokangyuan.com/",
        "title": "前去学习"
    }, {
        "avatar": "http://image.luokangyuan.com/4027734.jpeg",
        "name": "闪烁之狐",
        "introduction": "编程界大佬，技术牛，人还特别好，不懂的都可以请教大佬",
        "url": "https://blinkfox.github.io/",
        "title": "前去学习"
    }, {
        "avatar": "http://image.luokangyuan.com/avatar.jpg",
        "name": "ja_rome",
        "introduction": "平凡的脚步也可以走出伟大的行程",
        "url": "https://me.csdn.net/jlh912008548",
        "title": "前去学习"
    }]
    ```
### 1.2 菜单导航配置

> 关于导航的配置都在主题配置文件中

#### 1.2.1 配置基本菜单导航的名称、路径url和图标icon

- 导航名称可以设置成中文/英文
- 图标icon可以更换，具体属性值可以在[fontawesome](https://fontawesome.com/icons)中查找

```
menu:
  Index:
    url: /
    icon: fas fa-home
  Tags:
    url: /tags
    icon: fas fa-tags
  Categories:
    url: /categories
    icon: fas fa-bookmark
  Archives:
    url: /archives
    icon: fas fa-archive
  About:
    url: /about
    icon: fas fa-user-circle
  友人帐: #可以使用中文，也可以在对应的md中设置title:友人帐
    url: /friends
    icon: fas fa-address-book
```
#### 1.2.2 二级菜单配置方法

1. 在需要添加二级菜单的一级菜单下添加children关键字(如:爱好菜单下添加children)，一级菜单不需要增加url属性
2. 创建二级页面，步骤与创建页面步骤相同，编辑md时不需要`layout`属性
    ```
    ---
    title: 追番
    date: 2020-06-15 15:19:35
    type: "bangumis"
    ---
    ```
3. 给二级菜单增加名称name,路径url和图标icon
4. 注意每个二级菜单模块前要加 `-`
5. 二级菜单要缩进到一级菜单内
```
爱好:
    icon: fas fa-bicycle
    children:
      - name: 追番
        url: /bangumis
        icon: fas fa-play-circle
      - name: 音乐
        url: /musics
        icon: fas fa-music
```

#### 以网易云音乐为例

> 这个就非常简单了，不需要安装任何插件，只需要创建新页面，配置二级导航即可

1. 创建音乐页面
   
    输入命令
    
    ```
    hexo new page musics
    ```
    
    找到`source/musics/index.md`这个文件，修改这个文件，添加 `type: "music"`
    
    ```
    ---
    title: 音乐！音乐！
    date: 2020-06-16 14:45:30
    type: 'music'
    ---
    ```
    
    在index.md文件中增加以下内容
    
    ```
    <iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=530 height=520 src="//music.163.com/outchain/player?type=0&id=2817562565&auto=1&height=430"></iframe>
    ```
    
    > 第二行的id的那串数字，需要改成你想要的歌单id
    >
    > 查看自己id的方式：
    >
    > 1. 点击网易云音乐软件，找到想设置的歌单→分享→复制链接
    >
    > 2. [https://music.163.com/playlist?id=531558923&userid=375531677](https://music.163.com/playlist?id=531558923&userid=375531677)
    >
    > 3. id则是你想要的id，**不是**后面的userid
    >
    
2. 配置音乐页面为二级导航栏
   
    参考上边的二级导航栏配置方式
> 注意：此处界面最多显示十条歌曲，因此还存在问题
### 1.3 增加emoji支持

😄 使你markdown博客里的emoji表情跳动起来

1. 安装插件
   
    ```
    npm install hexo-filter-github-emojis --save
    ```
    
2. 在 Hexo 根目录下的 _config.yml 文件中，新增以下的配置项：
   
    ```
    githubEmojis:
      enable: true
      className: github-emoji
      inject: true
      styles:
      customEmojis:
    ```
    
    重新部署即可查看
    

> 小坑：
>
> 在配置支持前发布的文章中的表情并没有获得支持，并且连表情都不会显示，所以最好在配置之后再输入表情进行测试

### 1.4 新建文章自动打开本地Markdown编辑器
#### 1.4.1 新建文章模板

参考[Hexo-Matery主题细致美化(下)](https://marmalade.vip/Materysettings2.html)



##### 新建文章模板修改

首先为了新建文章方便，我们可以修改一下文章模板，可以将`/scaffolds/post.md`修改为如下代码：

front-matter

```front-matter
---
title: {{ title }}
date: {{ date }}
author: 
img: 
coverImg: 
top: false
cover: false
toc: true
mathjax: false
password:
summary:
keywords:
tags:
categories:
---
```

这样新建文章后 一些`Front-matter`参数不用你自己补充了，修改对应信息就可以了。

##### Front-matter 选项详解

`Front-matter` 选项中的所有内容均为**非必填**的。但原作者建议至少填写 `title` 和 `date` 的值。

| 配置选项      | 默认值                         | 描述                                                         |
| :------------ | :----------------------------- | :----------------------------------------------------------- |
| title         | `Markdown` 的文件标题          | 文章标题，强烈建议填写此选项                                 |
| date          | 文件创建时的日期时间           | 发布时间，强烈建议填写此选项，且最好保证全局唯一             |
| author        | 根 `_config.yml` 中的 `author` | 文章作者                                                     |
| img           | `featureImages` 中的某个值     | 文章特征图，推荐使用图床(腾讯云、七牛云、又拍云等)来做图片的路径.如: `http://xxx.com/xxx.jpg` |
| top           | `true`                         | 推荐文章（文章是否置顶），如果 `top` 值为 `true`，则会作为首页推荐文章 |
| cover         | `false`                        | `v1.0.2`版本新增，表示该文章是否需要加入到首页轮播封面中     |
| coverImg      | 无                             | `v1.0.2`版本新增，表示该文章在首页轮播封面需要显示的图片路径，如果没有，则默认使用文章的特色图片 |
| password      | 无                             | 文章阅读密码，如果要对文章设置阅读验证密码的话，就可以设置 `password` 的值，该值必须是用 `SHA256` 加密后的密码，防止被他人识破。前提是在主题的 `config.yml` 中激活了 `verifyPassword` 选项 |
| toc           | `true`                         | 是否开启 TOC，可以针对某篇文章单独关闭 TOC 的功能。前提是在主题的 `config.yml` 中激活了 `toc` 选项 |
| mathjax       | `false`                        | 是否开启数学公式支持 ，本文章是否开启 `mathjax`，且需要在主题的 `_config.yml` 文件中也需要开启才行 |
| summary       | 无                             | 文章摘要，自定义的文章摘要内容，如果这个属性有值，文章卡片摘要就显示这段文字，否则程序会自动截取文章的部分内容作为摘要 |
| categories    | 无                             | 文章分类，本主题的分类表示宏观上大的分类，只建议一篇文章一个分类 |
| tags          | 无                             | 文章标签，一篇文章可以多个标签                               |
| keywords      | 文章标题                       | 文章关键字，SEO 时需要                                       |
| reprintPolicy | cc_by                          | 文章转载规则， 可以是 cc_by, cc_by_nd, cc_by_sa, cc_by_nc, cc_by_nc_nd, cc_by_nc_sa, cc0, noreprint 或 pay 中的一个 |

##### 最全示例

front-matter

```front-matter
---
title: typora-vue-theme主题介绍
date: 2018-09-07 09:25:00
author: XX
img: /source/images/xxx.jpg
top: true
cover: true
coverImg: /images/1.jpg
password: 8d969eef6ecad3c29a3a629280e686cf0c3f5d5a86aff3ca12020c923adc6c92
toc: false
mathjax: false
summary: 这是你自定义的文章摘要内容，如果这个属性有值，文章卡片摘要就显示这段文字，否则程序会自动截取文章的部分内容作为摘要
categories: Markdown
tags:
  - Typora
  - Markdown
---
```




#### 1.4.2 自动打开本地Markdown编辑器

> 写新文章时，需要控制台执行hexo new “文章名字”生成一篇新文章，但需要手动打开，挺麻烦，我们可以设置在生成之后自动打开

在站点根目录下新建scripts目录，然后在新建`auto_open.js`，在文件填入一下内容：

```
var spawn = require('child_process').exec;

// Hexo 2.x 用户复制这段
//hexo.on('new', function(path){
  //spawn('start  "markdown编辑器绝对路径.exe" ' + path);
//});

// Hexo 3 用户复制这段
hexo.on('new', function(data){
  spawn('start  "D:\Program Files\Typora\Typora.exe" ' + data.path);
});
```

> 其中”D:\Program Files\Typora\Typora.exe”是我本地编辑器的路径，只需要改为你本地编辑器的路径即可，然后在执行`hexo cl && hexo g -d`，部署到GitHub即可，以后在发布文章就会自动打开编辑器。
### 1.5 代码高亮

由于 Hexo 自带的代码高亮主题显示不好看，用一个插件来替换它

1. 安装插件
   
    ```
    npm i -S hexo-prism-plugin
    ```
    
2. 修改 Hexo 站点配置文件 _config.yml 中 highlight.enable 的值为 false，并新增 prism 插件相关的配置，主要配置如下：
   
    ```
    prism_plugin:
      mode: 'preprocess'    # realtime/preprocess
      theme: 'tomorrow'
      line_number: false    # default false
      custom_css:
    ```
### 1.6 添加友链

在`\source\_data\friends.json`添加json字符串

欢迎小伙伴分享友链呀~

**Matery版：**

交换友链还请评论此格式哦~🌿

json

```json
{
    "avatar": "https://cdn.jsdelivr.net/gh/fenghen0918/fenghen0918.github.io/medias/logo.png",
    "name": "小苏の万事屋",
    "introduction": "一个不是只会写业务代码的后端攻城狮！",
    "url": "https://sulog.top/",
    "title": "前去关照"
}
```
### 1.7 搜索功能

实现文章内容搜索

1. 安装插件
   
    ```
    npm install hexo-generator-search --save
    ```
    
2. 在 Hexo 站点配置文件 _config.yml 中，新增以下的配置项：
   
    ```
    search:
      path: search.xml
      field: post
    ```
    

### 1.8 中文链接转拼音

如果你的文章名称是中文的，那么 Hexo 默认生成的文章链接也会有中文，这样不利于 SEO，且 gitment 评论对中文链接也不支持。我们可以用 hexo-permalink-pinyin Hexo 插件使在生成文章时生成中文拼音的永久链接。

1. 安装插件
   
    ```
    npm i hexo-permalink-pinyin --save
    ```
    
2. 在 Hexo 站点配置文件 _config.yml 中，新增以下的配置项：
   
    ```
    permalink_pinyin:
      enable: true
      separator: '-' # default: '-'
    ```
    

### 1.9 文章字数统计插件

用于在文章中显示文章字数、阅读时长信息

1. 安装插件
   
    ```
    npm i --save hexo-wordcount
    ```
    
2. 在**主题**配置文件_config.yml 文件中，**激活**以下配置项即可：
   
    ```
    wordCount:
      enable: false # 将这个值设置为 true 即可.
      postWordCount: true
      min2read: true
      totalCount: true
    ```
    

### 1.10 配置音乐播放器

想支持音乐播放，在**主题**的 _config.yml 配置文件中激活music配置即可：

```
# 是否在首页显示音乐.
music:
  enable: true
  title: #非吸底模式有效
    enable: true
    show: 听听音乐
  autoHide: false    # hide automaticaly
  server: netease   #require    music platform: netease, tencent, kugou, xiami, baidu
  type: playlist    #require song, playlist, album, search, artist
  id: 411680085     #require    song id / playlist id / album id / search keyword
  fixed: true       # 开启吸底模式
  autoplay: false   # 是否自动播放
  theme: '#42b983'
  loop: 'all'       # 音频循环播放, 可选值: 'all', 'one', 'none'
  order: 'random'   # 音频循环顺序, 可选值: 'list', 'random'
  preload: 'auto'   # 预加载，可选值: 'none', 'metadata', 'auto'
  volume: 0.7       # 默认音量，请注意播放器会记忆用户设置，用户手动设置音量后默认音量即失效
  listFolded: false  # 列表默认折叠
  hideLrc: true     # 隐藏歌词
```

> 属性介绍：
>
> server可选netease（网易云音乐），tencent（QQ音乐），kugou（酷狗音乐），xiami（虾米音乐），baidu（百度音乐）
>
> type可选song（歌曲），playlist（歌单），album（专辑），search（搜索关键字），artist（歌手）
>
> id获取示例: 浏览器打开网易云音乐，点击我喜欢的音乐歌单，地址栏有一串数字，playlist的id即为这串数字。

> 小坑：
>
> matery主题不支持pjax异步机制，在切换页面时音乐也会切换，不会继续一首歌播放
>
> 所以这个功能比较鸡肋，在于自己取舍

### 1.11 关于我页面添加个人简历

打开theme/matery/layout/about.ejs文件，大约在13行。有一个`card`标签，找出其对应结尾的标签，大约在61行左右，然后在下面新增如下代码

```
<div class="card">
     <div class="card-content">
         <div class="card-content article-card-content">
             <div class="title center-align" data-aos="zoom-in-up">
                 <i class="fa fa-address-book"></i>&nbsp;&nbsp;<%- __('个人简历') %>
              </div>
                 <div id="articleContent" data-aos="fade-up">
                     <%- page.content %>
                 </div>
           </div>
      </div>
</div>
```

注意粘贴的位置和空格要正确，这里的位置随你自己设置，你也可以把简历作为第一个card，然后/source/about/index.md下面写上你的简历了（就像写博客一样）。

> 中文显示为？？？
> 这是因为**站点配置文件**没有使用`utf-8`编码造成的，所以在**站点配置文件**`_config.yml`中写中文网站名，然后把**站点配置文件**保存为`utf-8格式`。包括md文件，出现该问题，也要用同样的方式解决。

### 1.12 配置404错误页面

站点根目录下的source文件夹下新建404.md文件，里面内容如下：

```
---
title: 404
date: 2020-6-18 16:41:10
type: "404"
layout: "404"
description: "Oops～，我崩溃了！找不到你想要的页面了"
---
```

在主题文件夹的layout目录下新建404.ejs文件，添加内容如下：

```
<style type="text/css">
    /* don't remove. */
    .about-cover {
        height: 90.2vh;
    }
</style>
<div class="bg-cover pd-header about-cover">
    <div class="container">
        <div class="row">
            <div class="col s10 offset-s1 m8 offset-m2 l8 offset-l2">
                <div class="brand">
                    <div class="title center-align">
                        404
                    </div>
                    <div class="description center-align">
                        <%= page.description %>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>

<script>
    // 每天切换 banner 图.  Switch banner image every day.
    $('.bg-cover').css('background-image', 'url(https://cdn.jsdelivr.net/gh/Yafine/cdn@3.3.1/source/medias/banner/' + new Date().getDay() + '.jpg)');
</script>
```

然后部署，再看看效果即可[http://localhost:4000/404/](http://localhost:4000/404/)

![image-20200619203902808](https://sulog.oss-cn-hangzhou.aliyuncs.com/matery2-6.png)



## 2. 视觉美化

### 2.1 修改主题颜色及导航透明效果

在主题文件的 /source/css/matery.css 文件中，搜索 .bg-color 来修改背景颜色：

```
/* 整体背景颜色，包括导航、移动端的导航、页尾、标签页等的背景颜色、透明效果. */
.bg-color {
    background-image: linear-gradient(to right, #4cbf30 0%, #0f9d58 100%);
    opacity: 0.8;  //透明效果 值范围 0~1，看情况自己修改
}
/*如果想去掉banner图的颜色渐变效果，请将以下的css属性注释掉或者删除掉即可*/
@-webkit-keyframes rainbow {
   /* 动态切换背景颜色. */
}
@keyframes rainbow {
    /* 动态切换背景颜色. */
}
```

### 2.2 修改主题页面
#### 2.2.1 修改 banner 图和文章特色图

你可以直接在 /source/medias/banner 文件夹中更换你喜欢的 banner 图片，主题代码中是每天动态切换一张，只需 7 张即可。

如果想改为每小时或者每分钟切换banner图的话，可以在 /layout/_partial/bg-cover-content.ejs 文件的 `bannerUrl` 代码中，将getDay()改为getHours()或者getMinutes()即可，当然需要再上述文件夹中有足够多的图片，如换成每小时就需要24张图。

```
var bannerUrl = "<%- theme.jsDelivr.url %><%- url_for('/medias/banner/') %>" + new Date().getDay() + '.jpg';
```
#### 2.2.2 整体背景修改

在`themes\Matery\source\css\matery.css`，ctrl+F快捷键查找`body`  
修改样式如下：
css

```css
body {
    /* background-color: #eaeaea; */
    background: linear-gradient(60deg, rgba(255, 165, 150, 0.5) 5%, rgba(0, 228, 255, 0.35)) 0% 0% / cover, url("https://ae01.alicdn.com/kf/H18a4b998752a4ae68b8e85d432a5aef0l.png"), url("https://ae01.alicdn.com/kf/H21b5f6b8496141a1979a33666e1074d9x.jpg") 0px 0px;
    background-attachment: fixed;
    margin: 0;
    color: #7F95D1;
}
```

#### 2.2.3 导航条颜色

修改`themes\Matery\source\css\matery.css`样式

快捷键ctrl+F查找定位到`#4cbf30`（浅绿色）和`#0f9d58`（深绿色）还有首页字体颜色，

然后将其修改为你喜欢的颜色

> 注意：不知有一处需要替换，建议将所有的都浅绿色和深绿色都替换成你的颜色
>
> 遇到的坑：
>
> 忘记修改这个，导致导航条颜色没有修改成功
>
> css
>
> ```css
> .bg-color {
>  background-image: linear-gradient(to right, #6DD0F2 0%, #F59ABE 100%);
>  opacity: 0.8;  /*透明效果 值范围 0~1，看情况自己修改*/
> }
> ```

#### 2.2.4 滚动条美化
此处为优化页面中所有的滚动条，包括代码横向的滚动条和页面纵向的滚动条

在`themes\Matery\source\css\matery.css`

样式添加如下：

css

```css
/* 滚动条 */
::-webkit-scrollbar-thumb {
    background-color: #FF2A68;
    background-image: -webkit-linear-gradient(45deg,rgba(255,255,255,.4) 25%,transparent 25%,transparent 50%,rgba(255,255,255,.4) 50%,rgba(255,255,255,.4) 75%,transparent 75%,transparent);
    border-radius: 3em;
}
::-webkit-scrollbar-track {
    background-color: #ffcacaff;
    border-radius: 3em;
}
::-webkit-scrollbar {
    width: 8px;
    height: 15px;
}
```

#### 2.2.5 目录透明化

增加样式在`themes\Matery\layout\_partial\post-detail-toc.ejs`

**修改**内容如下：

ejs

```ejs
.toc-widget {
width: 345px;
padding-left: 20px;
background-color: rgb(255, 255, 255,0.7);
border-radius: 10px;
box-shadow: 0 10px 35px 2px rgba(0, 0, 0, .15), 0 5px 15px rgba(0, 0, 0, .07), 0 2px 5px -5px rgba(0, 0, 0, .1) !important;
}
```


### 2.3 修改页脚、跳动红心

#### 2.3.1 跳动红心

1. 在文件的最下面加上以下代码
   
    ```
    <head><link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/HCLonely/images@master/others/heartbeat.min.css"></head>
    ```
    
2. 将需要加跳动红心的地方加上以下代码
   
    ```
    <i id="heartbeat" class="fa fas fa-heartbeat"></i>
    ```
    

#### 2.3.2 修改页脚

修改的地方`themes\matery\layout\_partial/footer.ejs`文件中，包括站点、使用的主题、访问量等。

![image-20200619215304130](https://sulog.oss-cn-hangzhou.aliyuncs.com/matery2-14.png)



我的配置：

```
<div class="col s12 m8 l8 copy-right">
    &copy;<span id="year"><%- theme.time.year %></span>-<span id="year"><%- theme.time.year +1 %></span>&nbsp;<i id="heartbeat" class="fa fas fa-heartbeat"></i>&nbsp;
    <a href="<%- url_for('/about') %>" target="_blank"><%- config.author %></a>
    <br>快乐每一天！
    <br>
<% if (theme.postInfo.totalCount) { %>
```
### 2.4 修改打赏二维码
在主题文件的 source/medias/reward 文件中，你可以替换成你的的微信和支付宝的打赏二维码图片。
### 2.5 修改社交链接

在主题配置文件_config.yml中，搜索`socialLink`，不配置值代表不启用，这是我的配置：

```
# 首页 banner 中的第二行个人信息配置，留空即不启用
socialLink:
  github:  https://github.com/fenghen0918
  email: 443175565@qq.com
  facebook: # https://www.facebook.com/xxx
  twitter: # https://twitter.com/xxx
  qq: 443175565
  weibo: # https://weibo.com/xxx
  zhihu: # https://www.zhihu.com/xxx
  rss:  # true、false
  weixin: https://cdn.jsdelivr.net/gh/fenghen0918/fenghen0918.github.io/medias/imgs/wechat.png
```

其中的weixin我是用的图片链接，会跳转到一个新的标签页，之后还需要修改ejs文件，文件在主题目录下的layout文件夹下的_partial文件夹，修改social-link.ejs，添加相关的配置，我个人添加的配置如下：

```
<% if (theme.socialLink.weixin) { %>
    <a href="<%= theme.socialLink.weixin %>" class="tooltipped" target="_blank" data-tooltip="微信联系我: " data-position="top" data-delay="50">
        <i class="fab fa-weixin"></i>
    </a>
<% } %>
```

### 2.6 动态标题

![image-20200619221831563](https://sulog.oss-cn-hangzhou.aliyuncs.com/matery2-15.png)



![image-20200619222009100](https://sulog.oss-cn-hangzhou.aliyuncs.com/matery2-16.png)



在主题文件下的`themes\matery\source\js`下新建`FunnyTitle.js`，增加以下代码

```
 var OriginTitle = document.title;
 var titleTime;
 document.addEventListener('visibilitychange', function () {
     if (document.hidden) {
         $('[rel="icon"]').attr('href', "https://cdn.jsdelivr.net/gh/Yafine/cdn@2.2/source/favicon.png");
         document.title = 'ヽ(●-`Д´-)ノ你要玩捉迷藏嘛';
         clearTimeout(titleTime);
     }
     else {
         $('[rel="icon"]').attr('href', "https://cdn.jsdelivr.net/gh/Yafine/cdn@2.2/source/favicon.png");
         document.title = 'ヾ(Ő∀Ő3)ノ好哦！' + OriginTitle;
         titleTime = setTimeout(function () {
             document.title = OriginTitle;
         }, 2000);
     }
 });
```

在`themes/matery/layout/layout.ejs`文件中添加如下代码：

```
  <script type="text/javascript">
        var OriginTitile=document.title,st;
        document.addEventListener("visibilitychange",function(){
            document.hidden?(document.title="ヽ(●-`Д´-)ノ你要玩捉迷藏嘛",clearTimeout(st)):(document.title="(Ő∀Ő3)ノ好哦！",st=setTimeout(function(){document.title=OriginTitile},3e3))
        })
    </script>
```

### 2.7 修改全局字体（局限：只有浏览器安装才能正常显示）

1. 在根目录下的 `source` 文件夹内创建一个名为 `font` 的文件夹，即文件夹路径为 `/source/font/` ，用来统一存放你要用到的字体。
   
2. 将你要用到的字体放入上述创建的文件夹内，字体名称最好为英文，如 /source/font/myFont.ttf
   
    > 字体下载推荐：[http://www.diyiziti.com/](http://www.diyiziti.com/)
    
3. 找到 `/themes/matery/source/css/`下的 my.css 文件，填入下面的代码：
   
    ```
    @font-face{
        font-family: 'myFont';
        src: url('../font/myFont.ttf');
    }
    
    body{
        font-family: 'myFont';
    }
    ```
     将上面的 myFont 改成你自己的字体名称即可
    修改字体的坑：
> 上传字体后网页不显示，找了很多方法，浏览器还是无法显示该字体
> 方法：为确保字体正常显示，注意此处为**所有用户安装**，而不是简单的安装
> ![](https://gitee.com/jgyong/blogimg/raw/master/img/202403241501409.png)
>
> 但还是不行23333
>
> 最后发现是自己的字体文件有问题，但是该字体可以在其他软件如Obsidian中正常显示，但是在浏览器中就是不行。
>
> 后来找了一下该字体的其他版本 [Screen](https://github.com/lxgw/LxgwWenKai-Screen/releases)，竟然可以显示了。。。。感觉有点玄学在里面。。。。。实在是搞不清楚原因。。。。



所以更好的方式是通过这种在线配置的方法[# 通过css的@font-face属性，在网页上显示用户电脑没有的字体。](https://blog.csdn.net/rsj1994/article/details/53037881#:~:text=%E5%9C%A8%E7%BD%91%E9%A1%B5%E4%B8%AD%EF%BC%8C%E6%88%91%E4%BB%AC%E5%8F%AF%E4%BB%A5%E7%94%A8CSS%E7%9A%84font-family%E5%B1%9E%E6%80%A7%E6%9D%A5%E5%AE%9A%E4%B9%89%E5%AD%97%E4%BD%93%EF%BC%8C%E7%84%B6%E8%80%8C%E5%AE%9A%E4%B9%89%E7%9A%84%E5%AD%97%E4%BD%93%E5%9C%A8%E7%94%A8%E6%88%B7%E7%9A%84%E7%94%B5%E8%84%91%E4%B8%8A%E8%83%BD%E5%90%A6%E6%AD%A3%E7%A1%AE%E5%91%88%E7%8E%B0%E5%88%99%E8%A6%81%E7%9C%8B%E7%94%A8%E6%88%B7%E7%9A%84%E7%94%B5%E8%84%91%E6%98%AF%E5%90%A6%E5%AE%89%E8%A3%85%E4%BA%86%E8%AF%A5%E5%AD%97%E4%BD%93%E3%80%82,%E6%88%91%E4%BB%AC%E7%BB%8F%E5%B8%B8%E8%83%BD%E7%9C%8B%E5%88%B0%E5%9B%BD%E5%A4%96%E7%9A%84%E4%B8%80%E4%BA%9B%E4%B8%AA%E4%BA%BA%E7%BD%91%E7%AB%99%E4%BD%BF%E7%94%A8%E4%BA%86%E9%9D%9E%E5%B8%B8%E6%BC%82%E4%BA%AE%E7%9A%84%E5%AD%97%E4%BD%93%EF%BC%8C%E8%80%8C%E8%BF%99%E4%BA%9B%E5%AD%97%E4%BD%93%E9%80%9A%E5%B8%B8%E5%9C%A8%E7%94%A8%E6%88%B7%E7%9A%84%E7%94%B5%E8%84%91%E4%B8%AD%E6%98%AF%E6%B2%A1%E6%9C%89%E5%AE%89%E8%A3%85%E7%9A%84%EF%BC%8C%E6%89%80%E4%BB%A5%E7%94%A8font-family%E5%B1%9E%E6%80%A7%E5%B0%B1%E6%97%A0%E6%B3%95%E5%AE%9E%E7%8E%B0%E4%BA%86%E3%80%82)，[# 如需网页上嵌入，请看这里](https://github.com/lxgw/LxgwWenKai/issues/24)由于时间关系，没有深入研究。

### 2.8 自定义鼠标样式

首先将鼠标样式下载到本地，推荐大家一个网站：[https://zhutix.com/ico/ori-cursors/](https://zhutix.com/ico/ori-cursors/)

以我的为例，我将鼠标指针样式放在了主题文件夹下的medias目录下，然后打开`themes\matery\source\css`下的**my.css**文件，添加内容如下：

```
*{
    cursor: url("/medias/imgs/zhengchang.ico"),auto!important;
}
:active{
    cursor: url("/medias/imgs/dianji.ico"),auto!important;
}
```
### 2.9 页面特效效果增加
个人认为效果还是动态彩带效果最好
#### 2.9.1 添加背景动态彩带效果
参考链接[# Hexo 博客美化合集（不断更新）](https://zhuanlan.zhihu.com/p/69211731)和[# Hexo-Sakura主题配置](https://kaizynx.github.io/2020/03/19/Sakura_setting/)，链接1提供的代码有误，与链接2提供的内容结合才可以实现该功能。
![](https://gitee.com/jgyong/blogimg/raw/master/img/202403241328890.png)
实现方法：在 \themes\material-x\layout\layout.ejs 文件的body前面添加如下代码：
```ejs
<script src="https://cdn.jsdelivr.net/gh/wallleap/cdn@latest/js/piao.js" type="text/javascript"></script>
```
还可以参考[# js代码为你得网站加入动态彩色飘带](https://iymark.com/articles/649.html)，将彩带文件更改为本地文件，此处未做尝试
#### 2.9.2 樱花飘落
此处作者博客中没有写相关代码，而且个人认为添加樱花效果反而显得页面很乱，这里没有记录
#### 2.9.3 背景动态科技线条
```
<!--动态线条背景-->
<script type="text/javascript"
color="122 103 238" opacity='0.7' zIndex="-2" count="200" src="//cdn.bootcss.com/canvas-nest.js/1.0.0/canvas-nest.min.js">
</script>
```
### 2.10 页面加载动画添加
主要按照博客[# Matery主题自定义(六)页面加载动画](https://blog.csdn.net/weixin_43662760/article/details/122311217)进行，建议访问原博客
1. 在 `themes>hexo-theme-matery>layout>_widget` 下创建一个 loading.ejs 文件，将下面的代码 cv 进去

```
<% if (theme.preloader.enable) { %>
  <div id="loading-box">
    <div class="loading-left-bg"></div>
    <div class="loading-right-bg"></div>
    <div class="spinner-box">
      <div class="configure-border-1">
        <div class="configure-core"></div>
      </div>
      <div class="configure-border-2">
        <div class="configure-core"></div>
      </div>
      <div class="loading-word">加载中...</div>
    </div>
  </div>
  <!-- 页面加载动画 -->
  <script>
    $(document).ready(function () {
      document.body.style.overflow = 'auto';
      document.getElementById('loading-box').classList.add("loaded")
    })
  </script>
<% } %>
```

2. 完成了结构代码，下面就开始样式代码了，不然没有样式的动画也太丑了，下面的就是样式代码
当然，在复制粘贴代码之前，需要先创建样式文件
在 themes>hexo-theme-matery>source>css> 下创建一个新的文件 loading.css，在将下面的代码复制粘贴

```
#loading-box .loading-left-bg,
#loading-box .loading-right-bg {
  position: fixed;
  z-index: 1000;
  width: 50%;
  height: 100%;
  background-color: #37474f;
  transition: all 0.5s;
}

#loading-box .loading-right-bg {
  right: 0;
}

#loading-box>.spinner-box {
  position: fixed;
  z-index: 1001;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100vh;
}

#loading-box .spinner-box .configure-border-1 {
  position: absolute;
  padding: 3px;
  width: 115px;
  height: 115px;
  background: #ffab91;
  animation: configure-clockwise 3s ease-in-out 0s infinite alternate;
}

#loading-box .spinner-box .configure-border-2 {
  left: -115px;
  padding: 3px;
  width: 115px;
  height: 115px;
  background: rgb(63, 249, 220);
  transform: rotate(45deg);
  animation: configure-xclockwise 3s ease-in-out 0s infinite alternate;
}

#loading-box .spinner-box .loading-word {
  position: absolute;
  color: #ffffff;
  font-size: 0.8rem;
}

#loading-box .spinner-box .configure-core {
  width: 100%;
  height: 100%;
  background-color: #37474f;
}

div.loaded div.loading-left-bg {
  transform: translate(-100%, 0);
}

div.loaded div.loading-right-bg {
  transform: translate(100%, 0);
}

div.loaded div.spinner-box {
  display: none !important;
}

@keyframes configure-clockwise {
  0% {
    transform: rotate(0);
  }

  25% {
    transform: rotate(90deg);
  }

  50% {
    transform: rotate(180deg);
  }

  75% {
    transform: rotate(270deg);
  }

  100% {
    transform: rotate(360deg);
  }
}

@keyframes configure-xclockwise {
  0% {
    transform: rotate(45deg);
  }

  25% {
    transform: rotate(-45deg);
  }

  50% {
    transform: rotate(-135deg);
  }

  75% {
    transform: rotate(-225deg);
  }

  100% {
    transform: rotate(-315deg);
  }
}

```

3. 添加至页面
在将加载动画添加至页面中
找到 themes>hexo-theme-matery>layout>_partial>head.ejs 文件，这个文件专门用来引入样式文件和配置网页信息

在 <head> 标签中引入 loading.css 文件

```
<link rel="stylesheet" type="text/css" href="<%- theme.jsDelivr.url %><%- url_for('/css/loading.css') %>">
```
引入样式文件后，引入结构文件 loading.ejs，插入在themes>hexo-theme-matery>layout>layout.ejs <body> 标签下第一行就行了
```
<%- partial('_widget/loading') %>
```
4. 配置
最后在主题配置文件中进行配置 _config.yml，true 是开启；false 是关闭

```
# 是否开启页面加载动画
preloader:
  enable: true
```
### 2.11 图片冒泡功能
同样是参考同一作者的博客[图片冒泡功能](https://blog.csdn.net/weixin_43662760/article/details/122311008)
1. 创建 buble.js
在 `themes>hexo-theme-matery>source>libs>others` 下创建一个新的文件 `buble.js`，将下面的代码 CV 到 `buble.js` 中

```
// 上升的气泡
function buble () {
  $('.carousel-item, .pd-header').circleMagic({
    radius: 10,
    density: .2,
    color: 'rgba(255,255,255,.4)',
    clearOffset: 0.99
  });
} ! function (p) {
  p.fn.circleMagic = function (t) {
    var o, a, n, r, e = !0,
      i = [],
      d = p.extend({
        color: "rgba(255,0,0,.5)",
        radius: 10,
        density: .3,
        clearOffset: .2
      }, t),
      l = this[0];
    function c () {
      e = !(document.body.scrollTop > a)
    }
    function s () {
      o = l.clientWidth, a = l.clientHeight, l.height = a + "px", n.width = o, n.height = a
    }
    function h () {
      if (e)
        for (var t in r.clearRect(0, 0, o, a), i) i[t].draw();
      requestAnimationFrame(h)
    }
    function f () {
      var t = this;
      function e () {
        t.pos.x = Math.random() * o, t.pos.y = a + 100 * Math.random(), t.alpha = .1 + Math.random() * d.clearOffset,
          t.scale = .1 + .3 * Math.random(), t.speed = Math.random(), "random" === d.color ? t.color =
            "rgba(" + Math.floor(255 * Math.random()) + ", " + Math.floor(0 * Math.random()) + ", " + Math.floor(
              0 * Math.random()) + ", " + Math.random().toPrecision(2) + ")" : t.color = d.color
      }
      t.pos = {}, e(), this.draw = function () {
        t.alpha <= 0 && e(), t.pos.y -= t.speed, t.alpha -= 5e-4, r.beginPath(), r.arc(t.pos.x, t.pos.y,
          t.scale * d.radius, 0, 2 * Math.PI, !1), r.fillStyle = t.color, r.fill(), r.closePath()
      }
    } ! function () {
      o = l.offsetWidth, a = l.offsetHeight,
        function () {
          var t = document.createElement("canvas");
          t.id = "canvas";
          t.style.top = 0;
          t.style.left = 0
          t.style.right = 0
          t.style.zIndex = 0;
          t.style.position = "absolute";

          l.appendChild(t);
          t.parentElement.style.overflow = "hidden"
        }(), (n = document.getElementById("canvas")).width = o, n.height = a, r = n.getContext("2d");
      for (var t = 0; t < o * d.density; t++) {
        var e = new f;
        i.push(e)
      }
      h()
    }(), window.addEventListener("scroll", c, !1), window.addEventListener("resize", s, !1)
  }
}(jQuery);
buble()
```
2. _config.yml 配置
接着将这个文件在主题的配置文件（_config.yml）中 lib:js: 下引入，大约在 458 行
```
buble: /libs/others/buble.js
```
在主题的配置文件（_config.yml）中添加下面的代码
```
# banner 冒泡
buble:
  enable: true
```
3. 引用
在 themes>hexo-theme-matery>layout>layout.ejs 这的 body 标签中添加下面的代码

```
<!-- 冒泡 -->
<% if (theme.buble.enable) { %>
    <script type="text/javascript">
        // 只在桌面版网页启用特效
        var windowWidth = $(window).width();
        document.write(
            '<script type="text/javascript" src="<%- theme.jsDelivr.url %><%- url_for(theme.libs.js.buble) %>"><\/script>'
        );
    </script>
<% } %>
```
banner 冒泡的效果就完成了
### 待优化功能
1. 夜间模式
2. 点击图片翻转
3. 通过在线配置字体的方式，使得未安装该字体的浏览器也能正常显示
## 3 博客优化
此处并未进行修改，工作放在以后
### 3.1 gulp代码压缩
>注意：由于gulp版本更新，老版本的设置方式不适用，此处未做优化
### 3.2 CDN加速

## 总结
此次主要依靠各位大佬的记录，优化博客界面，对于主题`matery`修改了一些样式，增加了一些功能。但对于前端页面的知识还是了解特别少，博客优化方面还有很多需要学习的地方，下面记录一下各位大佬的博客链接，方便以后优化页面，了解相关知识。再次感谢各位大佬的知识分享。
[# matery主题优化专栏](https://blog.csdn.net/weixin_43662760/category_11551976.html)
[# 【源码开放】Hexo+Github+Coding 博客butterfly 和 matery 主题 搭建完全教程【整理】](https://blog.csdn.net/weixin_42429718/article/details/105723193?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522171118467516800227433663%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fblog.%2522%257D&request_id=171118467516800227433663&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~first_rank_ecpm_v1~rank_v31_ecpm-1-105723193-null-null.nonecase&utm_term=matery&spm=1018.2226.3001.4450)

[魔改记录](https://fenghen0918.github.io/2020/10/22/hexo/hexo-bo-ke-you-hua-pian-matery-yi/#toc-heading-1)
[大佬原始文件](https://yafine66.gitee.io/posts/20200317173728-8c84.html)
