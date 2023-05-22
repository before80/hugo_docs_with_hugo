+++
title = "菜单模板"
weight = 17
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Menu Templates - 菜单模板 

[https://gohugo.io/templates/menu-templates/](https://gohugo.io/templates/menu-templates/)

​	在您的模板中使用菜单变量和方法来渲染菜单。

## 概述  

​	在[定义菜单条目](https://gohugo.io/content-management/menus/)之后，使用[菜单变量和方法](https://gohugo.io/variables/menus/)来渲染菜单。

​	有三个因素决定如何渲染菜单：

1. 定义菜单条目的方法：[自动定义](https://gohugo.io/content-management/menus/#define-automatically)、[在前置元数据中定义](https://gohugo.io/content-management/menus/#define-in-front-matter)或[在站点配置中定义](https://gohugo.io/content-management/menus/#define-in-site-configuration)
2. 菜单结构：平面或嵌套
3. 用于[本地化菜单条目](https://gohugo.io/content-management/multilingual/#menus)的方法：站点配置或翻译表

​	下面的示例处理了每种组合。

## 示例 

​	这个局部模板递归地"遍历"菜单结构，渲染本地化、可访问的嵌套列表。

layouts/partials/menu.html

```go-html-template
{{- $page := .page }}
{{- $menuID := .menuID }}

{{- with index site.Menus $menuID }}
  <nav>
    <ul>
      {{- partial "inline/menu/walk.html" (dict "page" $page "menuEntries" .) }}
    </ul>
  </nav>
{{- end }}

{{- define "partials/inline/menu/walk.html" }}
  {{- $page := .page }}
  {{- range .menuEntries }}
    {{- $attrs := dict "href" .URL }}
    {{- if $page.IsMenuCurrent .Menu . }}
      {{- $attrs = merge $attrs (dict "class" "active" "aria-current" "page") }}
    {{- else if $page.HasMenuCurrent .Menu .}}
      {{- $attrs = merge $attrs (dict "class" "ancestor" "aria-current" "true") }}
    {{- end }}
    <li>
      <a
        {{- range $k, $v := $attrs }}
          {{- with $v }}
            {{- printf " %s=%q" $k $v | safeHTMLAttr }}
          {{- end }}
        {{- end -}}
      >{{ or (T .Identifier) .Name | safeHTML }}</a>
      {{- with .Children }}
        <ul>
          {{- partial "inline/menu/walk.html" (dict "page" $page "menuEntries" .) }}
        </ul>
      {{- end }}
    </li>
  {{- end }}
{{- end }}
```

​	调用上面的局部，传递一个菜单ID和当前页面的上下文。

layouts/_default/single.html

```go-html-template
{{ partial "menu.html" (dict "menuID" "main" "page" .) }}
{{ partial "menu.html" (dict "menuID" "footer" "page" .) }}
```

## 页面引用 

​	无论您如何[定义菜单条目](https://gohugo.io/content-management/menus/)，与页面相关联的条目都可以访问页面变量和方法。

​	这个简单的示例在每个条目的`name`旁边渲染一个名为`version`的页面参数。使用`with`或`if`来处理(a) 指向外部资源的条目，或者(b) `version`参数未定义的条目。

layouts/_default/single.html

```go-html-template
{{- range site.Menus.main }}
  <a href="{{ .URL }}">
    {{ .Name }}
    {{- with .Page }}
      {{- with .Params.version -}}
        ({{ . }})
      {{- end }}
    {{- end }}
  </a>
{{- end }}
```

## 菜单条目参数 

当您在站点配置或前置元数据中定义菜单条目时，可以包括params键，如以下示例所示：

​	当您在[站点配置中](https://gohugo.io/content-management/menus/#define-in-site-configuration)定义菜单条目或[在前置元数据中](https://gohugo.io/content-management/menus/#define-in-front-matter)定义菜单条目时，您可以像这些示例中那样包含一个`params`键：

- [在站点配置中定义菜单条目 ](https://gohugo.io/content-management/menus/#example-site-configuration)
- [在前置元数据中定义菜单条目](https://gohugo.io/content-management/menus/#example-front-matter) 

​	这个简单的示例为每个锚点元素呈现一个`class`属性。使用`with`或`if`来处理`params.class`未定义的条目。

layouts/partials/menu.html

```go-html-template
{{- range site.Menus.main }}
  <a {{ with .Params.class -}} class="{{ . }}" {{ end -}} href="{{ .URL }}">
    {{ .Name }}
  </a>
{{- end }}
```

## 本地化 

​	Hugo提供了两种本地化菜单条目的方法。详见[多语言](https://gohugo.io/content-management/multilingual/#menus)。

## 另请参阅 

- [菜单 ](https://gohugo.io/content-management/menus/)
- [.GetPage](https://gohugo.io/functions/getpage/)
- [内容章节](https://gohugo.io/content-management/sections/)
- [内容类型 ](https://gohugo.io/content-management/types/)
- [Hugo中的内容列表](https://gohugo.io/templates/lists/)
