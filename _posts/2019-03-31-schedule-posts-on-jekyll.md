---
layout: post
title: How to schedule blog posts when using Jekyll with Github
author: fnds
categories: tools
tags: jekyll github
---

# How to schedule blog posts when using Jekyll and Github

1. Add this line to _config.yml

        future: false
    
    This changes causes Jekyll to ignore any posts with dates in the future

2. Create a post with the desired posting date

    2019-03-19-schedule-posts-on-jekyll.md
    
3. Schedule a task to force Gitgub to rebuild your site every night

    Use your favorite scheduler to execute this command line every night at your chosen time:
    
        curl "https://api.github.com/repos/USERNAME/REPO/pages/builds" \
        -X GET \
        -H 'Authorization: token THE-TOKEN' \
        -H "Accept: application/vnd.github.mister-fantastic-preview"

    Check this article for details on how to set this up: 
    
        - [How to Schedule Jekyll Posts on Github Pages](https://alxmjo.com/2017/05/30/how-to-schedule-posts-with-jekyll/)

This article was posted using the same scheduling solution. It works! :)

Thanks for reading.  
--fnds

## references

- [How to schedule posts with Jekyll](https://shot511.github.io/2018-12-03-how-to-schedule-posts-with-jekyll/)
- [How to Schedule Jekyll Posts on Github Pages](https://alxmjo.com/2017/05/30/how-to-schedule-posts-with-jekyll/)
