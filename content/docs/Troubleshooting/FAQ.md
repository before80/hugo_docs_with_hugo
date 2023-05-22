+++
title = "FAQ"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Frequently Asked Questions

[https://gohugo.io/troubleshooting/faq/](https://gohugo.io/troubleshooting/faq/)

Solutions to some common Hugo problems.

**Note:** The answers/solutions presented below are short, and may not be enough to solve your problem. Visit [Hugo Discourse](https://discourse.gohugo.io/) and use the search. It that does not help, start a new topic and ask your questions.

## I can’t see my content! 

Is your Markdown file [in draft mode](https://gohugo.io/content-management/front-matter/#front-matter-variables)? When testing, run `hugo server` with the `-D` or `--buildDrafts` [switch](https://gohugo.io/getting-started/usage/#draft-future-and-expired-content).

Is your Markdown file part of a [leaf bundle](https://gohugo.io/content-management/page-bundles/)? If there is an `index.md` file in the same or any parent directory then other Markdown files will not be rendered as individual pages.

## Can I set configuration variables via OS environment? 

Yes you can! See [Configure with Environment Variables](https://gohugo.io/getting-started/configuration/#configure-with-environment-variables).

## How do I schedule posts? 

1. Set `publishDate` in the page [Front Matter](https://gohugo.io/content-management/front-matter/) to a datetime in the future. If you want the creation and publication datetime to be the same, it’s also sufficient to only set `date`[1](https://gohugo.io/troubleshooting/faq/#fn:1).
2. Build and publish at intervals.

How to automate the "publish at intervals" part depends on your situation:

- If you deploy from your own PC/server, you can automate with [Cron](https://en.wikipedia.org/wiki/Cron) or similar.

- If your site is hosted on a service similar to

   

  Netlify

   

  you can:

  - Use a service such as [ifttt](https://ifttt.com/date_and_time) to schedule the updates
  - Set up a deploy hook which you can run with a cron service to deploy your site at intervals, such as [cron-job.org](https://cron-job.org/) (both Netlify and Cloudflare Pages support deploy hooks)

Also see this Twitter thread:

<iframe id="twitter-widget-0" scrolling="no" frameborder="0" allowtransparency="true" allowfullscreen="true" class="" title="Twitter Tweet" src="https://platform.twitter.com/embed/Tweet.html?dnt=false&amp;embedId=twitter-widget-0&amp;features=eyJ0ZndfdGltZWxpbmVfbGlzdCI6eyJidWNrZXQiOltdLCJ2ZXJzaW9uIjpudWxsfSwidGZ3X2ZvbGxvd2VyX2NvdW50X3N1bnNldCI6eyJidWNrZXQiOnRydWUsInZlcnNpb24iOm51bGx9LCJ0ZndfdHdlZXRfZWRpdF9iYWNrZW5kIjp7ImJ1Y2tldCI6Im9uIiwidmVyc2lvbiI6bnVsbH0sInRmd19yZWZzcmNfc2Vzc2lvbiI6eyJidWNrZXQiOiJvbiIsInZlcnNpb24iOm51bGx9LCJ0ZndfbWl4ZWRfbWVkaWFfMTU4OTciOnsiYnVja2V0IjoidHJlYXRtZW50IiwidmVyc2lvbiI6bnVsbH0sInRmd19leHBlcmltZW50c19jb29raWVfZXhwaXJhdGlvbiI6eyJidWNrZXQiOjEyMDk2MDAsInZlcnNpb24iOm51bGx9LCJ0ZndfZHVwbGljYXRlX3NjcmliZXNfdG9fc2V0dGluZ3MiOnsiYnVja2V0Ijoib24iLCJ2ZXJzaW9uIjpudWxsfSwidGZ3X3ZpZGVvX2hsc19keW5hbWljX21hbmlmZXN0c18xNTA4MiI6eyJidWNrZXQiOiJ0cnVlX2JpdHJhdGUiLCJ2ZXJzaW9uIjpudWxsfSwidGZ3X2xlZ2FjeV90aW1lbGluZV9zdW5zZXQiOnsiYnVja2V0Ijp0cnVlLCJ2ZXJzaW9uIjpudWxsfSwidGZ3X3R3ZWV0X2VkaXRfZnJvbnRlbmQiOnsiYnVja2V0Ijoib24iLCJ2ZXJzaW9uIjpudWxsfX0%3D&amp;frame=false&amp;hideCard=false&amp;hideThread=false&amp;id=962380712027590657&amp;lang=en&amp;origin=https%3A%2F%2Fgohugo.io%2Ftroubleshooting%2Ffaq%2F&amp;sessionId=bd55ce66d3456e7174587325e94b9c9374291c52&amp;siteScreenName=GoHugoIO&amp;theme=light&amp;widgetsVersion=aaf4084522e3a%3A1674595607486&amp;width=550px" style="visibility: hidden; width: 0px; height: 0px; display: block; flex-grow: 1;"></iframe>

> [@GoHugoIO](https://twitter.com/GoHugoIO?ref_src=twsrc^tfw) Converted https://t.co/icCzS7Ha7q from [@Medium](https://twitter.com/Medium?ref_src=twsrc^tfw) to Hugo yesterday. Once I figure out how to do scheduled posts I will be ecstatic.
>
> — Chris Short 🇺🇸🇺🇦 (@ChrisShort)
>
>  
>
> February 10, 2018

## Can I use the latest Hugo version on Netlify? 

Yes you can! Read [this](https://gohugo.io/hosting-and-deployment/hosting-on-netlify/#configure-hugo-version-in-netlify).

## I get "… this feature is not available in your current Hugo version" 

If you process `SCSS` or `Sass` to `CSS` in your Hugo project with `libsass` as the transpiler or if you convert images to the `webp` format, you need the Hugo `extended` version, or else you may see an error message similar to the below:

```bash
error: failed to transform resource: TOCSS: failed to transform "scss/main.scss" (text/x-scss): this feature is not available in your current Hugo version
```

We release two set of binaries for technical reasons. The extended version is not what you get by default for some installation methods. On the [release page](https://github.com/gohugoio/hugo/releases), look for archives with `extended` in the name. To build `hugo-extended`, use `go install --tags extended`

To confirm, run `hugo version` and look for the word `extended`.

------

1. See [Configure Dates](https://gohugo.io/getting-started/configuration/#configure-dates) for the order in which the different date variables are complemented by each other when not explicitly set. [↩︎](https://gohugo.io/troubleshooting/faq/#fnref:1)
