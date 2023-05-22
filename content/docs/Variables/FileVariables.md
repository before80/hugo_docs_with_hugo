+++
title = "文件变量"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# File Variables - 文件变量 

[https://gohugo.io/variables/files/](https://gohugo.io/variables/files/)

Use File variables to access file-related values for each page that is backed by a file.

使用文件变量来访问由文件支持的每个页面的与文件相关的值。 

​	使用文件变量来访问每个由文件支持的页面的与文件相关的值。

## 变量 

​	`.File.Path`、`.File.Dir` 和 `.File.Filename` 中的路径分隔符（斜杠或反斜杠）取决于操作系统。

### .File.Path

​	(`string`) 文件路径，相对于 `content` 目录。

### .File.Dir

​	(`string`) 不包括文件名的文件路径，相对于 `content` 目录。

### .File.LogicalName

​	(`string`) 文件名。

### .File.BaseFileName

​	(`string`) 不包括扩展名的文件名。

### .File.TranslationBaseName

​	(`string`) 不包括扩展名和语言标识符的文件名。

### .File.Ext

​	(`string`) 文件扩展名。

### .File.Lang

​	(`string`) 与给定文件相关联的语言。

### .File.ContentBaseName

​	(`string`) 如果页面是一个分支或叶子 bundle，则为包含该页面的目录名称，否则为 `.TranslationBaseName`。

### .File.Filename

​	(`string`) 绝对文件路径。

### .File.UniqueID

​	(`string`) `.File.Path` 的 MD5 哈希值。

## 示例

```text
content/
├── news/
│   ├── b/
│   │   ├── index.de.md   <-- leaf bundle
│   │   └── index.en.md   <-- leaf bundle
│   ├── a.de.md           <-- regular content
│   ├── a.en.md           <-- regular content
│   ├── _index.de.md      <-- branch bundle
│   └── _index.en.md      <-- branch bundle
├── _index.de.md
└── _index.en.md
```

​	使用上述内容结构，英文页面的 `.File` 对象包含以下属性：

|                     | regular content | leaf bundle        | branch bundle     |
| :------------------ | :-------------- | :----------------- | :---------------- |
| Path                | news/a.en.md    | news/b/index.en.md | news/_index.en.md |
| Dir                 | news/           | news/b/            | news/             |
| LogicalName         | a.en.md         | index.en.md        | _index.en.md      |
| BaseFileName        | a.en            | index.en           | _index.en         |
| TranslationBaseName | a               | index              | _index            |
| Ext                 | md              | md                 | md                |
| Lang                | en              | en                 | en                |
| ContentBase         | a               | b                  | news              |
| Filename            | /home/user/…    | /home/user/…       | /home/user/…      |
| UniqueID            | 15be14b…        | 186868f…           | 7d9159d…          |

## 防御性编程 

​	站点上的某些页面可能没有文件支持。例如：

- 顶级章节页面 
- 分类法页面 
- 条目页面 

​	如果您尝试访问 `.File` 属性而没有支持文件，Hugo 将抛出一个警告。例如：

```text
WARN .File.ContentBaseName on zero object. Wrap it in if or with...
```

​	为了防御性编程：

```go-html-template
{{ with .File }}
  {{ .ContentBaseName }}
{{ end }}
```

## 另请参阅 

- [Babel](https://gohugo.io/hugo-pipes/babel/)
- [Hugo 模板简介 ](https://gohugo.io/templates/introduction/)
- [本地文件模板 ](https://gohugo.io/templates/files/)
- [菜单变量 ](https://gohugo.io/variables/menus/)
- [高亮](https://gohugo.io/functions/highlight/)
