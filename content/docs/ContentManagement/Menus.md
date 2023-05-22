+++
title = "菜单"
weight = 17
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Menus - 菜单

[https://gohugo.io/content-management/menus/](https://gohugo.io/content-management/menus/)

​	通过定义条目、本地化每个条目以及渲染结果数据结构来创建菜单。 

## 概述  

​	要为您的站点创建菜单步骤如下：

1. 定义菜单条目 
3. [本地化](https://gohugo.io/content-management/multilingual/#menus)每个条目 
5. 使用[模板](https://gohugo.io/templates/menu-templates/)渲染菜单 

​	创建多个菜单，可以是平面或嵌套的。例如，创建一个用于页眉的主菜单，以及一个用于页脚的单独菜单。

​	有三种方法可以定义菜单条目：

1. 自动定义 
2. 在前置元数据中定义
3. 在站点配置中定义

​	虽然可以在定义菜单时结合使用这些方法，但如果在整个站点中使用一种方法，则更容易理解和维护菜单。

## 自动定义 

​	要为站点的每个顶级章节自动定义菜单条目，请在站点配置中启用section pages menu。

config.

=== "yaml"

    ``` yaml
    sectionPagesMenu: main
    
    ```

=== "toml"

    ``` toml
    sectionPagesMenu = 'main'
    
    ```

=== "json"

    ``` json
    {
       "sectionPagesMenu": "main"
    }
    
    ```



​	这将创建一个菜单结构，您可以在模板中使用 `site.Menus.main` 访问它。有关详细信息，请参阅[菜单模板](https://gohugo.io/templates/menu-templates/)。

## 在前置元数据中定义 

​	要将一个页面添加到"main"菜单中：

content/about.md

=== "yaml"

    ``` yaml
    ---
    menu: main
    title: About
    ---
    ```

=== "toml"

    ``` toml
    +++
    menu = 'main'
    title = 'About'
    +++
    ```

=== "json"

    ``` json
    {
       "menu": "main",
       "title": "About"
    }
    ```



​	您可以在模板中使用 `site.Menus.main` 访问该条目。有关详细信息，请参阅[菜单模板](https://gohugo.io/templates/menu-templates/)。

​	要将一个页面添加到"main"和"footer"菜单中：

content/contact.md

=== "yaml"

    ``` yaml
    ---
    menu:
    - main
    - footer
    title: Contact
    ---
    ```

=== "toml"

    ``` toml
    +++
    menu = ['main', 'footer']
    title = 'Contact'
    +++
    ```

=== "json"

    ``` json
    {
       "menu": [
          "main",
          "footer"
       ],
       "title": "Contact"
    }
    ```



​	您可以在模板中使用 `site.Menus.main` 和 `site.Menus.footer` 访问该条目。有关详细信息，请参阅[菜单模板](https://gohugo.io/templates/menu-templates/)。

### 属性 

​	在前置元数据中定义菜单条目时，请使用以下这些属性：

- identifier

  （`string`）当两个或多个菜单条目具有相同`name`或者使用翻译表（translation tables）本地化`name`时，必填。必须以字母开头，后跟字母、数字或下划线。 

- name

  （`string`）在渲染该菜单条目时要显示的文本。 

- params

  （`map`）该菜单条目的用户定义属性。 

- parent

  （`string`）该父菜单条目的`identifier`。如果未定义`identifier`，请使用`name`。在嵌套菜单中的子菜单条目中必填。 

- post

  （`string`）在渲染该菜单条目时追加的HTML。 

- pre

  （`string`）在渲染该菜单条目时前置的HTML。 

- title

  （`string`）被渲染的该菜单条目的HTML的`title`属性。 

- weight

  （`int`）非零整数，表示该条目相对于菜单根的位置，或者表示子条目相对于其父级的位置。较轻的条目上浮到顶部，较重的条目下沉到底部。 

### 示例 

​	此前置元数据菜单条目演示了一些可用属性：

content/products/software.md

=== "yaml"

    ``` yaml
    ---
    menu:
      main:
        params:
          class: center
        parent: Products
        pre: <i class="fa-solid fa-code"></i>
        weight: 20
    title: Software
    ---
    ```

=== "toml"

    ``` toml
    +++
    title = 'Software'
    [menu]
      [menu.main]
        parent = 'Products'
        pre = '<i class="fa-solid fa-code"></i>'
        weight = 20
        [menu.main.params]
          class = 'center'
    +++
    ```

=== "json"

    ``` json
    {
       "menu": {
          "main": {
             "params": {
                "class": "center"
             },
             "parent": "Products",
             "pre": "\u003ci class=\"fa-solid fa-code\"\u003e\u003c/i\u003e",
             "weight": 20
          }
       },
       "title": "Software"
    }
    ```



​	在模板中使用`site.Menus.main`访问该条目。有关详细信息，请参见[菜单模板](https://gohugo.io/templates/menu-templates/)。

## 在站点配置中定义 

​	要定义"main"菜单的条目：

config.

=== "yaml"

    ``` yaml
    menu:
      main:
      - name: Home
        pageRef: /
        weight: 10
      - name: Products
        pageRef: /products
        weight: 20
      - name: Services
        pageRef: /services
        weight: 30
    ```

=== "toml"

    ``` toml
    [menu]
    [[menu.main]]
      name = 'Home'
      pageRef = '/'
      weight = 10
    [[menu.main]]
      name = 'Products'
      pageRef = '/products'
      weight = 20
    [[menu.main]]
      name = 'Services'
      pageRef = '/services'
      weight = 30
    ```

=== "json"

    ``` json
    {
       "menu": {
          "main": [
             {
                "name": "Home",
                "pageRef": "/",
                "weight": 10
             },
             {
                "name": "Products",
                "pageRef": "/products",
                "weight": 20
             },
             {
                "name": "Services",
                "pageRef": "/services",
                "weight": 30
             }
          ]
       }
    }
    ```



​	这将创建一个菜单结构，您可以在模板中使用`site.Menus.main`访问。有关详细信息，请参见[菜单模板](https://gohugo.io/templates/menu-templates/)。

​	要定义"footer"菜单的条目：

config.

=== "yaml"

    ``` yaml
    menu:
      footer:
      - name: Terms
        pageRef: /terms
        weight: 10
      - name: Privacy
        pageRef: /privacy
        weight: 20
    ```

=== "toml"

    ``` toml
    [menu]
    [[menu.footer]]
      name = 'Terms'
      pageRef = '/terms'
      weight = 10
    [[menu.footer]]
      name = 'Privacy'
      pageRef = '/privacy'
      weight = 20
    ```

=== "json"

    ``` json
    {
       "menu": {
          "footer": [
             {
                "name": "Terms",
                "pageRef": "/terms",
                "weight": 10
             },
             {
                "name": "Privacy",
                "pageRef": "/privacy",
                "weight": 20
             }
          ]
       }
    }
    ```



​	这将创建一个菜单结构，您可以在模板中使用`site.Menus.footer`访问。有关详细信息，请参见[菜单模板](https://gohugo.io/templates/menu-templates/)。

### 属性 

​	[在前置元数据中定义的条目可用的属性](https://gohugo.io/content-management/menus/#properties-front-matter)也适用于在站点配置中定义的条目。

​	在站点配置中定义的每个菜单条目都需要两个或多个属性：

- 为内部链接指定`name`和`pageRef`
- 为外部链接指定`name`和`url` 

- pageRef

  （`string`）目标页面的文件路径，相对于`content`目录。省略语言代码和文件扩展名。内部链接则必填。 

| Kind     | pageRef         |
| :------- | :-------------- |
| home     | `/`             |
| page     | `/books/book-1` |
| section  | `/books`        |
| taxonomy | `/tags`         |
| term     | `/tags/foo`     |

- url

  （`string`）外部链接则必填。

### 示例

​	这个嵌套菜单演示了一些可用的属性：

config.

=== "yaml"

    ``` yaml
    menu:
      main:
      - name: Products
        pageRef: /products
        weight: 10
      - name: Hardware
        pageRef: /products/hardware
        parent: Products
        weight: 1
      - name: Software
        pageRef: /products/software
        parent: Products
        weight: 2
      - name: Services
        pageRef: /services
        weight: 20
      - name: Hugo
        params:
          rel: external
        pre: <i class="fa fa-heart"></i>
        url: https://gohugo.io/
        weight: 30
    ```

=== "toml"

    ``` toml
    [menu]
    [[menu.main]]
      name = 'Products'
      pageRef = '/products'
      weight = 10
    [[menu.main]]
      name = 'Hardware'
      pageRef = '/products/hardware'
      parent = 'Products'
      weight = 1
    [[menu.main]]
      name = 'Software'
      pageRef = '/products/software'
      parent = 'Products'
      weight = 2
    [[menu.main]]
      name = 'Services'
      pageRef = '/services'
      weight = 20
    [[menu.main]]
      name = 'Hugo'
      pre = '<i class="fa fa-heart"></i>'
      url = 'https://gohugo.io/'
      weight = 30
      [menu.main.params]
        rel = 'external'
    ```

=== "json"

    ``` json
    {
       "menu": {
          "main": [
             {
                "name": "Products",
                "pageRef": "/products",
                "weight": 10
             },
             {
                "name": "Hardware",
                "pageRef": "/products/hardware",
                "parent": "Products",
                "weight": 1
             },
             {
                "name": "Software",
                "pageRef": "/products/software",
                "parent": "Products",
                "weight": 2
             },
             {
                "name": "Services",
                "pageRef": "/services",
                "weight": 20
             },
             {
                "name": "Hugo",
                "params": {
                   "rel": "external"
                },
                "pre": "\u003ci class=\"fa fa-heart\"\u003e\u003c/i\u003e",
                "url": "https://gohugo.io/",
                "weight": 30
             }
          ]
       }
    }
    ```



​	这将创建一个菜单结构，您可以在模板中使用 `site.Menus.main` 访问。有关详细信息，请参阅[菜单模板](https://gohugo.io/templates/menu-templates/)。

## 本地化 

​	Hugo提供了两种方法来本地化菜单条目。请参阅[多语言](https://gohugo.io/content-management/multilingual/#menus)。

## 渲染 

​	请参阅[菜单模板](https://gohugo.io/templates/menu-templates/)。

## 另请参阅  

- [菜单模板 ](https://gohugo.io/templates/menu-templates/)
- [.HasMenuCurrent](https://gohugo.io/functions/hasmenucurrent/)
- [.IsMenuCurrent](https://gohugo.io/functions/ismenucurrent/)
- [构建选项 ](https://gohugo.io/content-management/build-options/)
- [菜单变量](https://gohugo.io/variables/menus/)
