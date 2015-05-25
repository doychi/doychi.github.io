---
title: Jekyll Setup for Use with GitHub Pages
---
# Jekyll for Use with GitHub Pages

## Setup
Simple steps to setup Jekyll for use with Githup pages on Debian.

1. Install ruby `sudo aptitude install ruby`
1. Install jekyll `sudo aptitude install jekyll`
1. Install github-pages `sudo gem github-pages`
1. Create your GitHub Pages following the instructions on [GitHub Pages](https://pages.github.com)

## Using Jekyll to Test Your Site
```
bundle exec jekyll server --watch
```

I use this command because the for me the Jekyll server didn't automatically
watch the directories/files and update.

## Useful Links
[Bitwiser](http://bitwiser.in/2014/09/10/bitwiser-jekyll-theme.html)
