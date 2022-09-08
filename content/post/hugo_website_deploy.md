---
title: "Hugo website deployment"
date: 2022-09-08T18:23:37+08:00
draft: false
tags : ["Github", "Hugo"]
---

# Hugo website host on GitHub

Must prepare a ready-to-publish Hugo website.

Add following YAML content to **.github/workflows/gh-pages.yml**

```yaml
name: github pages

on:
  push:
    branches:
      - main  # Set a branch to deploy
  pull_request:

jobs:
  deploy:
    runs-on: ubuntu-20.04
    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true  # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'
          # extended: true

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        if: github.ref ** 'refs/heads/main'
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

# Ready to Push
Now push everything to **<username>.github.io** repo under **main** branch

You might get some error during **build with jekyll** stage like 

`
github-pages 227 | Error:  Liquid syntax error (line 135): Unknown tag 'image'
`
    
Just add an empty file named .nojekyll to the project 

> If you publish your site from a source branch, GitHub Pages will use Jekyll to build your site by default. If you want to use a static site generator other than Jekyll, we recommend that you write a GitHub Actions to build and publish your site instead. Otherwise, disable the Jekyll build process by creating an empty file called .nojekyll in the root of your publishing source, then follow your static site generator's instructions to build your site locally.... [Github](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#user--organization-pages)