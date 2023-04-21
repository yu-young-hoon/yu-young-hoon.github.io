---
layout: default
title: git hash는 어떻게 만들어지나
parent: git
nav_order: 700110
---

$ (printf "commit %s\0" $(git cat-file commit HEAD | wc -c); git cat-file commit HEAD) | sha1sum

https://gist.github.com/masak/2415865
