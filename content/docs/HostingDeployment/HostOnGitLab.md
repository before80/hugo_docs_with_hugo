+++
title = "Host on GitLab"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Host on GitLab

[https://gohugo.io/hosting-and-deployment/hosting-on-gitlab/](https://gohugo.io/hosting-and-deployment/hosting-on-gitlab/)

GitLab makes it easy to build, deploy, and host your Hugo website via their free GitLab Pages service, which provides native support for Hugo.

## Assumptions 

- Working familiarity with Git for version control
- Completion of the Hugo [Quick Start](https://gohugo.io/getting-started/quick-start/)
- A [GitLab account](https://gitlab.com/users/sign_in)
- A Hugo website on your local machine that you are ready to publish

## BaseURL 

The `baseURL` in your [site configuration](https://gohugo.io/getting-started/configuration/) must reflect the full URL of your GitLab pages repository if you are using the default GitLab Pages URL (e.g., `https://<YourUsername>.gitlab.io/<your-hugo-site>/`) and not a custom domain.

## Configure GitLab CI/CD 

Define your [CI/CD](https://docs.gitlab.com/ee/ci/quick_start/) jobs by creating a `.gitlab-ci.yml` file in the root of your project.

.gitlab-ci.yml



```yml
image: registry.gitlab.com/pages/hugo/hugo_extended:latest

variables:
  GIT_SUBMODULE_STRATEGY: recursive

pages:
  script:
  - hugo
  artifacts:
    paths:
    - public
  rules:
  - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH
```

See [this list](https://gitlab.com/pages/hugo/container_registry) if you wish to use a particular Hugo version to build your site.

## Push your Hugo website to GitLab 

Next, create a new repository on GitLab. It is *not* necessary to make the repository public. In addition, you might want to add `/public` to your .gitignore file, as there is no need to push compiled assets to GitLab or keep your output website in version control.

```bash
# initialize new git repository
git init

# add /public directory to our .gitignore file
echo "/public" >> .gitignore

# commit and push code to master branch
git add .
git commit -m "Initial commit"
git remote add origin https://gitlab.com/YourUsername/your-hugo-site.git
git push -u origin master
```

## Wait for your page to build 

That’s it! You can now follow the CI agent building your page at `https://gitlab.com/<YourUsername>/<your-hugo-site>/pipelines`.

After the build has passed, your new website is available at `https://<YourUsername>.gitlab.io/<your-hugo-site>/`.

## Next steps 

GitLab supports using custom CNAME’s and TLS certificates. For more details on GitLab Pages, see the [GitLab Pages setup documentation](https://about.gitlab.com/2016/04/07/gitlab-pages-setup/).

## 另请参阅

- [Host on Azure Static Web Apps](https://gohugo.io/hosting-and-deployment/hosting-on-azure/)
- [Host on Netlify](https://gohugo.io/hosting-and-deployment/hosting-on-netlify/)
- [Host on GitHub](https://gohugo.io/hosting-and-deployment/hosting-on-github/)
- [Host on KeyCDN](https://gohugo.io/hosting-and-deployment/hosting-on-keycdn/)
- [Host on Render](https://gohugo.io/hosting-and-deployment/hosting-on-render/)
