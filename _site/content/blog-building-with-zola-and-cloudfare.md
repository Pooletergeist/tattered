+++
title = "Free static sites with Zola and Cloudfare"
date = 2022-02-11

[taxonomies]
categories = ["How-to"]
+++

# Blog-building with Zola

## (we love rust)

### ((so much))

### Meaningless Recipe Pre-amble
I tried jekyll and github pages for 20ish hours. It didn't go well.
I saw two friends with zola blogs ([1](https://nihilistkitten.me/) \& [2](https://willm.how/blog/site-notes/)) and thought "what the heck?" Turns out, Zola is great. Cloudflare has a nice hook for it, and it all just sorta works.

# Requirements
- [Zola](https://www.getzola.org/) (for building the site)
- [Github](https://github.com/) (for backups and hosting)
- [Cloudfare](https://developers.cloudflare.com/pages/framework-guides/deploy-a-zola-site/#deploying-with-cloudflare-pages) (for hosting)

# Instructions 
Follow [Zola's excellent documentation](https://www.getzola.org/documentation/getting-started/overview/) or my bastardization:

1. make the zola site
```
zola init [optional directory name]
```

2. serve it
typing:
```
zola serve
```
from your main directory (the one with **config.toml**) lets you test things locally. Visit your site at: [http://127.0.0.1:1111](http://127.0.0.1:1111)

3. deploy it
[Cloudfare's lovely docs](https://developers.cloudflare.com/pages/framework-guides/deploy-a-zola-site/#deploying-with-cloudflare-pages)

 
## Helpful tips
- Make sure your ZOLA\_VERSION variable in Cloudflare's advanced options is 14.0 or earlier.

- add themes as submodules so Cloudflare clones them when it hosts your site.

# Adding Content
Inside the content folder, create markdown (.md) files. They'll show up!
From your site's main directory (the one with **config.toml**), 
```
vi content/first.md
```
Then edit to your hearts galore! As long as you have the right header:
```
+++
title = "some title"
+++
your text goes here!
```

## Adding a Theme
[Zola themes](https://www.getzola.org/themes/)
Each theme has its own special installation instructions but most require 2 things.
1. Add the theme to your repository. Git submodules are your friend here. If we were adding the theme "after-dark":
```
cd themes
git submodule add https://github.com/getzola/after-dark.git
```
2. Add the theme name to your **config.toml** file in your main directory. Anywhere in the top section usually works.
```
theme = "after-dark"
```
