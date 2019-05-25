---
title: "git"
layout: post
date: 2019-05-12 12:34
image: /assets/images/markdown.jpg
headerImage: false
tag:
- git
category: blog
author: zuewang
description: git notes
---

# update repo

### show remote url
git remote -v

### modify remote url
git remote set-url <name: e.g. upstream> <url>

### fetch upstream
git remote add upstream <git url>
git fetch upstream fetch all branches
git checkout master
git rebase upstream/master
git push -f origin master
