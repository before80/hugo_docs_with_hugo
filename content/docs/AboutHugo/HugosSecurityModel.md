+++
title = "Hugo 的安全模型"
weight = 1
date = 2023-05-22T13:22:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++
# Hugo's Security Model - Hugo 的安全模型 

https://gohugo.io/about/security-model/

Hugo 安全模型的概述。 

## 运行时安全 

​	Hugo 生成静态输出，因此一旦构建完成，运行时就是浏览器（假设输出为 HTML）和任何与之集成的服务器（API）。

​	但在开发和构建站点时，运行时是 `hugo` 可执行文件。保护运行时可能是[一个真正的挑战](https://blog.logrocket.com/how-to-protect-your-node-js-applications-from-malicious-dependencies-5f2e60ea08f9/)。

​	Hugo 的主要方法是沙盒化和采用严格默认的安全策略：

- Hugo 有一个虚拟文件系统，只有主项目（而不是第三方组件）可以挂载项目根目录外的目录或文件。 
- 只有主项目可以遍历符号链接。 
- 用户定义的组件只能以只读方式访问文件系统。 
- 我们调用一些外部二进制文件来支持 [Asciidoctor](https://gohugo.io/content-management/formats/#list-of-content-formats)等功能，但这些二进制文件及其标志都是预定义的，并且默认情况下被禁用（请参见以下安全策略）。运行任意外部操作系统命令的一般函数[已经讨论过](https://github.com/gohugoio/hugo/issues/796)，但由于安全问题而未实现。 

## 安全策略 

​	Hugo 具有内置的安全策略，限制对 [os/exec](https://pkg.go.dev/os/exec)、远程通信等的访问。

​	默认配置如下。任何使用安全策略允许列表中不存在的功能构建都将失败，并显示详细的消息，说明需要进行哪些操作。这些设置大多是允许列表（字符串或切片、[正则表达式](https://pkg.go.dev/regexp)或`none`不匹配任何内容）。

=== "yaml"

    ```yaml
    security:
      enableInlineShortcodes: false
      exec:
        allow:
        - ^dart-sass-embedded$
        - ^go$
        - ^npx$
        - ^postcss$
        osEnv:
        - (?i)^((HTTPS?|NO)_PROXY|PATH(EXT)?|APPDATA|TE?MP|TERM|GO\w+)$
      funcs:
        getenv:
        - ^HUGO_
        - ^CI$
      http:
        methods:
        - (?i)GET|POST
        urls:
        - .*
    ```

=== "toml"

    ```toml
    [security]
      enableInlineShortcodes = false
      [security.exec]
        allow = ['^dart-sass-embedded$', '^go$', '^npx$', '^postcss$']
        osEnv = ['(?i)^((HTTPS?|NO)_PROXY|PATH(EXT)?|APPDATA|TE?MP|TERM|GO\w+)$']
      [security.funcs]
        getenv = ['^HUGO_', '^CI$']
      [security.http]
        methods = ['(?i)GET|POST']
        urls = ['.*']
    ```

=== "json"

    ```json
    {
       "security": {
          "enableInlineShortcodes": false,
          "exec": {
             "allow": [
                "^dart-sass-embedded$",
                "^go$",
                "^npx$",
                "^postcss$"
             ],
             "osEnv": [
                "(?i)^((HTTPS?|NO)_PROXY|PATH(EXT)?|APPDATA|TE?MP|TERM|GO\\w+)$"
             ]
          },
          "funcs": {
             "getenv": [
                "^HUGO_",
                "^CI$"
             ]
          },
          "http": {
             "methods": [
                "(?i)GET|POST"
             ],
             "urls": [
                ".*"
             ]
          }
       }
    }
    ```

​	注意，Hugo 中的这些和其他配置设置可以被操作系统环境覆盖。如果您想阻止所有远程 HTTP 获取数据：

```txt
HUGO_SECURITY_HTTP_URLS=none hugo
```

## 依赖安全性 

​	Hugo 作为一个静态二进制文件使用 [Go Modules](https://github.com/golang/go/wiki/Modules) 来管理其依赖项。Go Modules 有几个保障措施，其中之一是 `go.sum` 文件。这是所有依赖项（包括传递依赖项）的预期密码校验和的数据库。

​	[Hugo Modules](https://gohugo.io/hugo-modules/) 是在 Go Modules 的功能之上构建的一个功能。像 Go Modules 一样，使用 Hugo Modules 的 Hugo 项目将有一个 `go.sum` 文件。我们建议将此文件提交到您的版本控制系统中。如果存在校验和不匹配，则 Hugo 构建将失败，这将表明[依赖项被篡改](https://julienrenaux.fr/2019/12/20/github-actions-security-risk/)。

## Web 应用程序安全性 

​	以下是 [OWASP](https://en.wikipedia.org/wiki/OWASP)定义的安全威胁。

​	对于 HTML 输出，这是核心安全模型：

https://pkg.go.dev/html/template#hdr-Security_Model

简而言之：

​	模板和配置作者（您）是可信任的，但您发送的数据不是。这就是为什么有时需要使用安全函数，如 `safeHTML`，以避免转义您知道是安全的数据。正如文档中所指出的一样，上述规则有一个例外：如果您启用内联shortcode，您也表明在内容文件中shortcode和数据处理是可信的，因为这些宏被视为纯文本。值得一提的是，Hugo 是一个静态站点生成器，没有动态用户输入的概念。

​	对于内容， 默认的 Markdown 渲染器[配置](https://gohugo.io/getting-started/configuration-markup)为删除或转义潜在的不安全内容。如果您信任自己的内容，则可以重新配置此行为。

## 另请参阅 ： 

- [Hugo 与通用数据保护条例（GDPR）](../HugoAndGDPR)