+++
title = "Deployment with Rclone"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Deployment with Rclone

[https://gohugo.io/hosting-and-deployment/deployment-with-rclone/](https://gohugo.io/hosting-and-deployment/deployment-with-rclone/)

If you have access to your web host with SFTP/FTP/SSH/HTTP(DAV), you can use rclone to incrementally deploy your entire Hugo website.

## Assumptions 

- A web host running a web server. This could be a shared hosting environment or a VPS.
- Access to your web host with any of the [protocols supported by rclone](https://rclone.org/#providers), such as SFTP.
- A functional static website built with Hugo
- Deploying from an [Rclone](https://rclone.org/) compatible operating system
- You have [installed Rclone](https://rclone.org/install/).

**NB**: You can remove `--interactive` in the commands below once you are comfortable with rclone, if you wish. Also, `--gc` and `--minify` are optional in the `hugo` commands below.

## Getting Started 

The spoiler is that you can even deploy your entire website from any compatible OS with no configuration. Using SFTP for example:

```txt
hugo --gc --minify
rclone sync --interactive --sftp-host sftp.example.com --sftp-user www-data --sftp-ask-password public/ :sftp:www/
```

## Configure Rclone for Even Easier Usage 

The easiest way is simply to run `rclone config`.

The [Rclone docs](https://rclone.org/docs/) provide [an example of configuring Rclone to use SFTP](https://rclone.org/sftp/).

For the next commands, we will assume you configured a remote you named `hugo-www`

The above ‘spoiler’ commands could become:

```txt
hugo --gc --minify
rclone sync --interactive public/ hugo-www:www/
```

After you issue the above commands (and respond to any prompts), check your website and you will see that it is deployed.

## 另请参阅

- [Deployment with Rsync](https://gohugo.io/hosting-and-deployment/deployment-with-rsync/)
- [Host on Azure Static Web Apps](https://gohugo.io/hosting-and-deployment/hosting-on-azure/)
- [Host on GitLab](https://gohugo.io/hosting-and-deployment/hosting-on-gitlab/)
- [Host on KeyCDN](https://gohugo.io/hosting-and-deployment/hosting-on-keycdn/)
- [Host on Netlify](https://gohugo.io/hosting-and-deployment/hosting-on-netlify/)
