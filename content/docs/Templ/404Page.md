+++
title = "自定义404页面"
weight = 16
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Custom 404 Page - 自定义404页面 

[https://gohugo.io/templates/404/](https://gohugo.io/templates/404/)

​	如果您知道如何创建单页模板，那么您可以无限制地创建自定义404页面。 

​	当使用 Hugo 与 [GitHub Pages](https://pages.github.com/) 时，可以通过在 `layouts` 文件夹的根目录中创建 `404.html` 模板文件来提供 [自定义的404 错误页面](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-custom-404-page-for-your-github-pages-site)。当 Hugo 生成您的站点时，`404.html` 文件将被放置在根目录中。

​	404 页面将拥有可用于模板的所有常规[页面变量](https://gohugo.io/variables/page/)。

​	除了标准页面变量外，404 页面还可以从 `.Pages` 访问所有站点内容。 

```txt
▾ layouts/
    404.html
```

## 404.html 

​	这是一个基本的404.html模板示例：

​	以下是一个基本的 `404.html` 模板示例：

layouts/404.html

```go-html-template
{{ define "main" }}
  <main id="main">
    <div>
      <h1 id="title"><a href="{{ "" | relURL }}">Go Home</a></h1>
    </div>
  </main>
{{ end }}
```

## 自动加载 

​	您的 `404.html` 文件可以在访问者输入错误的 URL 路径时自动加载，具体取决于您正在使用的 Web 服务器环境。例如：

- [GitHub Pages](https://gohugo.io/hosting-and-deployment/hosting-on-github/) 和 [GitLab Pages](https://gohugo.io/hosting-and-deployment/hosting-on-gitlab/)。404 页面是自动的。
- Apache。您可以在站点根目录的 `.htaccess` 文件中指定 `ErrorDocument 404 /404.html`。
- Nginx。您可以在 `nginx.conf` 文件中指定 `error_page 404 /404.html;`。[详情在此](https://nginx.org/en/docs/http/ngx_http_core_module.html#error_page)。
- Amazon AWS S3。在为静态 Web 服务设置存储桶时，您可以从 S3 GUI 中指定错误文件。
- Amazon CloudFront。您可以在 CloudFront 控制台的错误页面章节指定页面。[详情在此](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/custom-error-pages.html)。
- Caddy Server。使用 `handle_errors` 指令为一个或多个状态码指定错误页面。[详情在此](https://caddyserver.com/docs/caddyfile/directives/handle_errors)。
- Netlify。在 `content/_redirects` 中添加 `/* /404.html 404`。[详情在此](https://www.netlify.com/docs/redirects/#custom-404)
- Azure Static Web App。在配置文件 `staticwebapp.config.json` 中设置 `responseOverrides.404.rewrite` 和 `responseOverrides.404.statusCode`。[详情在此](https://docs.microsoft.com/en-us/azure/static-web-apps/configuration#response-overrides)
- Azure Storage 作为静态站点托管。您可以在 Azure 门户的静态站点配置页中指定`Error document path`。[详情在此](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blob-static-website)。
- DigitalOcean App 平台。您可以在应用程序规范文件中指定 `error_document` 或使用控制面板设置错误文档。[详情在此](https://docs.digitalocean.com/products/app-platform/how-to/manage-static-sites/#configure-a-static-site)。
- [Firebase Hosting](https://firebase.google.com/docs/hosting/full-config#404)：`/404.html` 自动用作404页面。

​	`hugo server` 不会自动加载您的自定义 `404.html` 文件，但是您可以通过将浏览器导航到`/404.html`来测试您的自定义"not found"页面的外观。
