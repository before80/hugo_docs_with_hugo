+++
title = "Host on GitHub"
weight = 7
date = 2023-05-18T17:03:08+08:00
description = ""
isCJKLanguage = true
draft = false
+++

# Host on GitHub

[https://gohugo.io/hosting-and-deployment/hosting-on-github/](https://gohugo.io/hosting-and-deployment/hosting-on-github/)

Deploy Hugo as a GitHub Pages project or personal/organizational site and automate the whole process with Github Actions

GitHub provides free and fast static hosting over SSL for personal, organization, or project pages directly from a GitHub repository via its GitHub Pages service and automating development workflows and build with GitHub Actions.

## Prerequisites 

1. [Create a GitHub account](https://github.com/signup)
2. [Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
3. [Create a Hugo site](https://gohugo.io/getting-started/quick-start/) and test it locally with `hugo server`.

## Types of sites 

There are three types of GitHub Pages sites: project, user, and organization. Project sites are connected to a specific project hosted on GitHub. User and organization sites are connected to a specific account on GitHub.com.

See the [GitHub Pages documentation](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#types-of-github-pages-sites) to understand the requirements for repository ownership and naming.

## Procedure 

- Step 1

  Create a GitHub repository.

- Step 2

  Push your local repository to GitHub.

- Step 3

  Visit your GitHub repository. From the main menu choose **Settings** > **Pages**. In then center of your screen you will see this:

![screen capture](HostOnGitHub_img/gh-pages-1.png)

- Step 4

  Change the **Source** to `GitHub Actions`. The change is immediate; you do not have to press a Save button.

![screen capture](HostOnGitHub_img/gh-pages-2.png)

- Step 5

  Create an empty file in your local repository.

```text
.github/workflows/hugo.yaml
```

- Step 6

  Copy and paste the YAML below into the file you created. Change the branch name and Hugo version as needed.

.github/workflows/hugo.yaml



```yaml
# Sample workflow for building and deploying a Hugo site to GitHub Pages
name: Deploy Hugo site to Pages

on:
  # Runs on pushes targeting the default branch
  push:
    branches:
      - main

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

# Allow only one concurrent deployment, skipping runs queued between the run in-progress and latest queued.
# However, do NOT cancel in-progress runs as we want to allow these production deployments to complete.
concurrency:
  group: "pages"
  cancel-in-progress: false

# Default to bash
defaults:
  run:
    shell: bash

jobs:
  # Build job
  build:
    runs-on: ubuntu-latest
    env:
      HUGO_VERSION: 0.111.3
    steps:
      - name: Install Hugo CLI
        run: |
          wget -O ${{ runner.temp }}/hugo.deb https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.deb \
          && sudo dpkg -i ${{ runner.temp }}/hugo.deb          
      - name: Install Dart Sass Embedded
        run: sudo snap install dart-sass-embedded
      - name: Checkout
        uses: actions/checkout@v3
        with:
          submodules: recursive
          fetch-depth: 0
      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v3
      - name: Install Node.js dependencies
        run: "[[ -f package-lock.json || -f npm-shrinkwrap.json ]] && npm ci || true"
      - name: Build with Hugo
        env:
          # For maximum backward compatibility with Hugo modules
          HUGO_ENVIRONMENT: production
          HUGO_ENV: production
        run: |
          hugo \
            --gc \
            --minify \
            --baseURL "${{ steps.pages.outputs.base_url }}/"          
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v1
        with:
          path: ./public

  # Deployment job
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v2
```

- Step 7

  Commit the change to your local repository with a commit message of something like "Add workflow", and push to GitHub.

- Step 8

  From GitHub’s main menu, choose **Actions**. You will see something like this:

![screen capture](HostOnGitHub_img/gh-pages-3.png)

- Step 9

  When GitHub has finished building and deploying your site, the color of the status indicator will change to green.

![screen capture](HostOnGitHub_img/gh-pages-4.png)

- Step 10

  Click on the commit message as shown above. You will see this:

![screen capture](HostOnGitHub_img/gh-pages-5.png)

Under the deploy step, you will see a link to your live site.

In the future, whenever you push a change from your local repository, GitHub will rebuild your site and deploy the changes.

## Additional resources 

- [Learn more about GitHub Actions](https://docs.github.com/en/actions)
- [Caching dependencies to speed up workflows](https://docs.github.com/en/actions/using-workflows/caching-dependencies-to-speed-up-workflows)
- [Manage a custom domain for your GitHub Pages site](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages)

## 另请参阅

- [Host on 21YunBox](https://gohugo.io/hosting-and-deployment/hosting-on-21yunbox/)
- [Host on Azure Static Web Apps](https://gohugo.io/hosting-and-deployment/hosting-on-azure/)
- [Host on GitLab](https://gohugo.io/hosting-and-deployment/hosting-on-gitlab/)
- [Host on AWS Amplify](https://gohugo.io/hosting-and-deployment/hosting-on-aws-amplify/)
- [Host on KeyCDN](https://gohugo.io/hosting-and-deployment/hosting-on-keycdn/)
