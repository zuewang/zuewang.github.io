---
title: "Linux"
layout: post
date: 2019-05-12 12:34
image: /assets/images/markdown.jpg
headerImage: false
tag:
- Linux
category: blog
author: zuewang
description: Linux notes
---

# X server for non-root user
in user1(root user) shell: cat ~/.Xauthority | sudo -u user2 -i tee .Xauthority > /dev/null su - user2 (reference: https://unix.stackexchange.com/questions/108784/running-gui-application-as-another-non-root-user)

# Save terminal output to file and also display output in console
tee
https://askubuntu.com/questions/420981/how-do-i-save-terminal-output-to-a-file
