---
layout: post
title:  "Creating a blog with Jekyll"
date:   2018-06-03 18:00:00 -0300
categories: tutorial jekyll
---
In this post I'm writing how to create a blog using Jekyll for to host in github.
This tutorial was created watching the Jekyll's course by Willian Justen in Udemy.

## Installing Jekyll
```bash
$ sudo apt install ruby

$ sudo apt install ruby-dev

$ sudo apt install ruby-bundler

$ sudo gem install jekyll

$ sudo gem install minima
```

## Creating a Blog
```bash
$ jekyll new name-of-your-blog

$ cd name-of-your-blog

$ jekyll build

$ jekyll s
```

## Creating a Blog with your look
```bash
$ jekyll new name-of-your-blog

$ cd name-of-your-blog

$ cp -rf $(bundle show minima)/* .

$ bundle exec jekyll build

$ bundle exec jekyll s
```

## Extras
```bash
jekyll --help

bundle show minima
```