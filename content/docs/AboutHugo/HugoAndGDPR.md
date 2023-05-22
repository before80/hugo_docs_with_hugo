+++
title = "Hugo and GDPR"
weight = 2
date = 2023-05-22T13:22:08+08:08
description = ""
isCJKLanguage = true
draft = false
+++
# Hugo and the General Data Protection Regulation (GDPR)

https://gohugo.io/about/hugo-and-gdpr/

​	关于如何配置您的 Hugo 站点以符合新的法规。

​	《一般数据保护条例》（[GDPR](https://en.wikipedia.org/wiki/General_Data_Protection_Regulation)）是欧盟法律中关于所有在欧盟和欧洲经济区内的个人数据保护和隐私的规定。它于2018年5月25日开始生效。

​	Hugo 是一个静态站点生成器。通过使用 Hugo，您已经站在了非常坚实的地面上。与服务器和数据库驱动的站点相比，磁盘上的静态 HTML 文件要容易理解得多。

​	但即使是静态站点也可以与外部服务集成，因此从版本`0.41`开始，Hugo提供了一个**隐私配置**，涵盖了相关的内置模板。

请注意：

- 这些设置默认设置为*off*，即 Hugo `0.41`之前的工作方式。您必须对您的站点进行评估，并应用适当的设置。
- 这些设置适用于[内部模板](https://gohugo.io/templates/internal/)。一些主题可能包含用于嵌入 Google Analytics 等服务的自定义模板。在这种情况下，这些选项将没有效果。 
- 我们将继续这项工作，并在未来的 Hugo 版本中进一步改进。

## 所有隐私设置 

​	以下是所有隐私设置及其默认值。这些设置需要放置在您的站点配置文件中（例如 `config.toml`）。

=== "yaml"

    ```yaml
    privacy:
      disqus:
        disable: false
      googleAnalytics:
        anonymizeIP: false
        disable: false
        respectDoNotTrack: false
        useSessionStorage: false
      instagram:
        disable: false
        simple: false
      twitter:
        disable: false
        enableDNT: false
        simple: false
      vimeo:
        disable: false
        enableDNT: false
        simple: false
      youtube:
        disable: false
        privacyEnhanced: false
    ```

=== "toml"

    ```toml
    [privacy]
      [privacy.disqus]
        disable = false
      [privacy.googleAnalytics]
        anonymizeIP = false
        disable = false
        respectDoNotTrack = false
        useSessionStorage = false
      [privacy.instagram]
        disable = false
        simple = false
      [privacy.twitter]
        disable = false
        enableDNT = false
        simple = false
      [privacy.vimeo]
        disable = false
        enableDNT = false
        simple = false
      [privacy.youtube]
        disable = false
        privacyEnhanced = false
    ```

=== "json"

    ```json
    {
       "privacy": {
          "disqus": {
             "disable": false
          },
          "googleAnalytics": {
             "anonymizeIP": false,
             "disable": false,
             "respectDoNotTrack": false,
             "useSessionStorage": false
          },
          "instagram": {
             "disable": false,
             "simple": false
          },
          "twitter": {
             "disable": false,
             "enableDNT": false,
             "simple": false
          },
          "vimeo": {
             "disable": false,
             "enableDNT": false,
             "simple": false
          },
          "youtube": {
             "disable": false,
             "privacyEnhanced": false
          }
       }
    }
    ```



## 禁用所有服务 

​	一个禁用Hugo中所有相关服务的隐私配置示例。使用此配置，其他设置将不会生效。

=== "yaml"

    ```yaml
    privacy:
      disqus:
        disable: true
      googleAnalytics:
        disable: true
      instagram:
        disable: true
      twitter:
        disable: true
      vimeo:
        disable: true
      youtube:
        disable: true
    ```

=== "toml"

    ```toml
    [privacy]
      [privacy.disqus]
        disable = true
      [privacy.googleAnalytics]
        disable = true
      [privacy.instagram]
        disable = true
      [privacy.twitter]
        disable = true
      [privacy.vimeo]
        disable = true
      [privacy.youtube]
        disable = true
    ```

=== "json"

    ```json
    {
       "privacy": {
          "disqus": {
             "disable": true
          },
          "googleAnalytics": {
             "disable": true
          },
          "instagram": {
             "disable": true
          },
          "twitter": {
             "disable": true
          },
          "vimeo": {
             "disable": true
          },
          "youtube": {
             "disable": true
          }
       }
    }
    ```





## 隐私设置的说明 

### GoogleAnalytics 

- anonymizeIP

  启用此选项将使用户的 IP 地址在 Google Analytics 中匿名化。 

- respectDoNotTrack

  启用此选项将使 GA 模板遵循"Do Not Track"HTTP标头。 

- useSessionStorage

  启用此选项将禁用使用 Cookies，并使用 Session Storage 存储 GA 客户端 ID。 

​	使用 Google Analytics v4（gtag.js）时不支持 `useSessionStorage`。

### Instagram 

- simple

  如果启用simple 模式，将构建 Instagram 图像卡的静态和无 JS 版本。请注意，这仅支持图像卡，并且图像本身将从 Instagram 的服务器获取。 

注意：如果您使用 Instagram 的simple模式和一个使用 Bootstrap 4 样式的站点，则可能需要禁用 Hugo 提供的内联样式。

=== "yaml"

    ```yaml
    services:
      instagram:
        disableInlineCSS: true
    ```

=== "toml"

    ```toml
    [services]
      [services.instagram]
        disableInlineCSS = true
    ```

=== "json"

    ```json
    {
       "services": {
          "instagram": {
             "disableInlineCSS": true
          }
       }
    }
    ```



### Twitter 

- enableDNT

  启用此选项后，Twitter/Tweet短代码中的推文及其在您站点上的嵌入页面不会用于包括个性化建议和个性化广告在内的用途。 

- simple

  如果启用simple模式，则会构建一个静态且不包含JavaScript的推文版本。 

注意：如果您在Twitter中使用simple模式，并且站点使用Bootstrap 4进行样式设置，则可能需要禁用Hugo提供的内联样式。

=== "yaml"

    ```
    services:
      twitter:
        disableInlineCSS: true
    ```

=== "toml"

    ```toml
    [services]
      [services.twitter]
        disableInlineCSS = true
    ```

=== "json"

    ```
    {
       "services": {
          "twitter": {
             "disableInlineCSS": true
          }
       }
    }
    ```



### YouTube 

- privacyEnhanced

  启用隐私增强模式后，YouTube将不会存储与访问者有关的信息，除非用户播放嵌入的视频。 

### Vimeo 

- enableDNT

  启用此选项后，Vimeo shortcode会阻止Vimeo播放器跟踪任何会话数据，包括所有cookie和统计数据。 

- simple

  如果启用简单模式，则会从Vimeo的服务器获取视频缩略图，并在其上覆盖一个播放按钮。如果用户点击播放视频，则会在新标签页中直接打开Vimeo站点中的视频。 

## 另请参阅 

- [Shortcodes](https://gohugo.io/content-management/shortcodes/)
- [配置Hugo](https://gohugo.io/getting-started/configuration/)
- [Hugo的安全模型l](https://gohugo.io/about/security-model/)