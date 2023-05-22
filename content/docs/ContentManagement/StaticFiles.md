+++
title = "静态文件"
weight = 18
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Static Files - 静态文件 

https://gohugo.io/content-management/static-files/

​	这些文件以静态方式（原样、无修改）在站点根目录上提供服务。 

​	默认情况下，站点项目中的 `static/` 目录用于所有静态文件（例如样式表、JavaScript、图像）。这些静态文件将在站点根路径上提供服务（例如，如果您有 `static/image.png` 文件，则可以使用 `http://{server-url}/image.png` 访问它，在文档中包含它可以使用`![Example image](/image.png) )`。 

​	Hugo 可以通过在[站点配置](https://gohugo.io/getting-started/configuration/#all-configuration-settings)中配置 `staticDir` 参数来查找不同的目录，甚至多个目录以获取这些静态文件。所有静态目录中的所有文件将组成一个联合文件系统。

​	这个联合文件系统将从您的站点根目录提供服务。因此，`<SITE PROJECT>/static/me.png` 文件将作为 `<MY_BASEURL>/me.png` 文件访问。

​	这里是一个为多语言站点设置 `staticDir` 和 `staticDir2` 的示例：

config.

=== "yaml"

    ``` yaml
    languages:
      en:
        baseURL: https://example.com
        languageName: English
        staticDir2: static_en
        title: In English
        weight: 2
      "no":
        baseURL: https://example.no
        languageName: Norsk
        staticDir:
        - staticDir_override
        - static_no
        title: På norsk
        weight: 1
    staticDir:
    - static1
    - static2
    ```

=== "toml"

    ``` toml
    staticDir = ['static1', 'static2']
    [languages]
      [languages.en]
        baseURL = 'https://example.com'
        languageName = 'English'
        staticDir2 = 'static_en'
        title = 'In English'
        weight = 2
      [languages.no]
        baseURL = 'https://example.no'
        languageName = 'Norsk'
        staticDir = ['staticDir_override', 'static_no']
        title = 'På norsk'
        weight = 1
    ```

=== "json"

    ``` json
    {
       "languages": {
          "en": {
             "baseURL": "https://example.com",
             "languageName": "English",
             "staticDir2": "static_en",
             "title": "In English",
             "weight": 2
          },
          "no": {
             "baseURL": "https://example.no",
             "languageName": "Norsk",
             "staticDir": [
                "staticDir_override",
                "static_no"
             ],
             "title": "På norsk",
             "weight": 1
          }
       },
       "staticDir": [
          "static1",
          "static2"
       ]
    }
    ```



​	在上面的示例中，未使用任何主题：

- 英文站点将其静态文件作为"static1"、"static2"和"static_en"的联合体。对于文件重复，右边的版本将获胜。 
- 挪威站点将其静态文件作为"staticDir_override"和"static_no"的联合体。 

- Note 1

  `staticDir2` 中的 `2`（可以是 0 到 10 的数字）被添加以告诉 Hugo 您想将此目录添加到使用 `staticDir` 定义的全局静态目录集合中。在语言级别上使用 `staticDir` 将替换全局值（如挪威站点案例所示）。 

- Note 2

  上面的示例是一个[multihost设置](https://gohugo.io/content-management/multilingual/#configure-multilingual-multihost)。在常规设置中，所有静态目录将对所有站点都可用。  

## 另请参阅  

- [配置模块 ](https://gohugo.io/hugo-modules/configuration/)
- [目录结构 ](https://gohugo.io/getting-started/directory-structure/)
- [主题组件 ](https://gohugo.io/hugo-modules/theme-components/)
- [使用 Hugo 模块 ](https://gohugo.io/hugo-modules/use-modules/)
- [本地文件模板](https://gohugo.io/templates/files/)
