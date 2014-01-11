---
layout: post
title:  "Blogging with Github Pages and Jekyll"
date:   2013-12-31 05:11:25
categories: jekyll github
author: trey
---

This blog is hosted by [Github Pages][ghpages], a useful way to make websites using git. Github will host anything you throw into a repository named *yourname*.github.io (this will also serve as your domain).

In addition to hosting static web content, Github Pages has native support for [Jekyll][jekyll], a Ruby server specially designed for generating static web content. You can just push the Jekyll project files to your repository and Github will use Jekyll on their servers to process the files into a website. You'll get an email from Github if your site fails to build.

If you use the [editing features][ghflow] built into Github, you can have a web interface for posting to your blog. Just go into the `_posts` folder and click the little `+` icon to the right of the folder name. Write up a blog post in markdown, then commit it. The page will show up on your site within about 10 minutes.

[ghpages]: http://pages.github.com
[jekyll]: http://jekyllrb.com
[ghflow]: https://github.com/blog/1557-github-flow-in-the-browser

