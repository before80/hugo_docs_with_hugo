+++
title = "主题组件"
weight = 3
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Theme Components - 主题组件 

https://gohugo.io/hugo-modules/theme-components/

​	Hugo 提供了主题组件的高级主题支持。 

> ​	本部分包含的信息可能已过时，并正在重写过程中。

​	从 Hugo `0.42` 版本开始，项目可以将主题配置为所需的多个主题组件的组合：

config.

=== "yaml"

    ```yaml
    theme:
    - my-shortcodes
    - base-theme
    - hyde
    ```

=== "toml"

    ```toml
    theme = ['my-shortcodes', 'base-theme', 'hyde']
    ```

=== "json"

    ```json
    {
       "theme": [
          "my-shortcodes",
          "base-theme",
          "hyde"
       ]
    }
    ```

​	甚至可以嵌套使用，主题组件本身可以在其 own `config.toml` 中包含主题组件 (主题继承)。[1](https://gohugo.io/hugo-modules/theme-components/#fn:1)

​	上述 `config.toml` 中的主题定义示例创建了一个具有从左到右优先级的三个主题组件的主题。

​	对于任何给定的文件、数据条目等，Hugo 将首先查找项目，然后查找 `my-shortcodes`、`base-theme`，最后是 `hyde`。

​	Hugo 使用两种不同的算法来合并文件系统，具体取决于文件类型：

- 对于 `i18n` 和`data`文件，Hugo 使用文件内部的翻译 ID 和数据键进行深度合并。 
- 对于`static`文件、`layouts` (templates) 和`archetypes`文件，这些文件在文件级别上进行合并。所以最左边的文件将被选中。 

​	上面的`theme`定义中使用的名称必须与 `/your-site/themes` 中的一个文件夹相匹配，例如 `/your-site/themes/my-shortcodes`。计划改进此功能，并获取 URL 方案，以便可以自动解析。

​	还要注意，作为主题的组件可以有自己的配置文件，例如 `config.toml`。目前，主题组件可以配置的内容存在一些限制：

- `params` (global and per language)
- `menu` (global and per language)
- `outputformats` and `mediatypes`

​	这里也适用相同的规则：具有相同 ID 的最左边的 param/menu 等将获胜。上述内容中还存在一些隐藏的实验性命名空间支持，我们将在未来努力改进，但鼓励主题作者创建自己的命名空间，以避免命名冲突。

------

1. 对于托管在 [Hugo Themes Showcase](https://themes.gohugo.io/)中的主题组件，需要将组件添加为 git 子模块，指向目录 `exampleSite/themes`。 ↩︎

## 另请参阅 

- [配置模块 ](https://gohugo.io/hugo-modules/configuration/)
- [使用 Hugo 模块 ](https://gohugo.io/hugo-modules/use-modules/)
- [目录结构 ](https://gohugo.io/getting-started/directory-structure/)
- [静态文件 ](https://gohugo.io/content-management/static-files/)
- [将您的 Hugo 主题添加到展示中](https://gohugo.io/contribute/themes/)
