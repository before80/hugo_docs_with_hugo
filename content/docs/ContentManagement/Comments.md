+++
title = "评论"
weight = 20
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Comments - 评论

​	Hugo内置了Disqus模板，但这不是唯一能够与您的新Hugo站点配合使用的评论系统。 

​	Hugo支持[Disqus](https://disqus.com/)，这是一个第三方服务，通过JavaScript为站点提供评论和社区功能。

​	您的主题可能已经支持Disqus，但如果没有，可以通过[Hugo内置的Disqus partial](https://gohugo.io/templates/internal/#disqus)轻松添加到您的模板中。

## 添加Disqus 

​	Hugo已经为您的模板提供了加载Disqus所需的所有代码。在将Disqus添加到您的站点之前，您需要[设置一个帐户](https://disqus.com/profile/signup/)。

### 配置Disqus 

​	Disqus评论要求您在[站点的配置文件](https://gohugo.io/getting-started/configuration/)中设置单个值，如下所示：

=== "yaml"

    ``` yaml
    disqusShortname: yourDisqusShortname
    
    ```

=== "toml"

    ``` toml
    disqusShortname = 'yourDisqusShortname'
    
    ```

=== "json"

    ``` json
    {
       "disqusShortname": "yourDisqusShortname"
    }
    
    ```



​	对于许多站点来说，这样的配置已经足够。但是，您还可以在单个内容文件的[前置元数据](https://gohugo.io/content-management/front-matter/)中设置以下内容：

- `disqus_identifier`
- `disqus_title`
- `disqus_url`

### 渲染Hugo内置的Disqus部分模板 

​	Disqus有其自己的[内部模板](https://gohugo.io/templates/internal/#disqus)可用，要渲染它，请在要出现评论的位置添加以下代码：

```go-html-template
{{ template "_internal/disqus.html" . }}
```

## 替代方案 

以下是Disqus的一些替代方案：

- [Cactus Comments](https://cactus.chat/docs/integrations/hugo/)（开源，Matrix appservice，Docker安装） 
- [Commento](https://commento.io/)（开源，可用作服务，本地安装或docker映像） 
- [Graph Comment](https://graphcomment.com/)
- [Hyvor Talk](https://talk.hyvor.com/)（可用作服务） 
- [IntenseDebate](https://intensedebate.com/)
- [Isso](https://isso-comments.de/)（自托管，Python）（[tutorial](https://stiobhart.net/2017-02-24-isso-comments/)） 
- [Muut](https://muut.com/)
- [Remark42](https://remark42.com/)（开源，Golang，易于运行docker） 
- [ReplyBox](https://getreplybox.com/)
- [Staticman](https://staticman.net/)
- [Talkyard](https://blog-comments.talkyard.io/)（开源，无服务器托管） 
- [Utterances](https://utteranc.es/)（开源，基于GitHub问题构建的GitHub评论小部件） 

## 另请参阅  

- [内容组织 ](https://gohugo.io/content-management/organization/)
- [内容章节](https://gohugo.io/content-management/sections/)
- [内容类型 ](https://gohugo.io/content-management/types/)
- [.GetPage](https://gohugo.io/functions/getpage/)
- [构建选项](https://gohugo.io/content-management/build-options/)
