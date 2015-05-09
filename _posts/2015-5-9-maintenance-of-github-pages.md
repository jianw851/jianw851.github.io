---
layout: post
category: trick
title:  Maintenance of github pages 
tagline: by Jian
tags: [jekyll,git,ruby,rails,maintenance]
---
   I am a new learner, content bellow will show some tricks about github pages' development and maintenance. How to use  git, jekyll, ruby, rails will also be included.

<!--more-->

###Recovery
$ git log --pretty=oneline
this is to look formal commit
$ git reset --hard 1a410efbd13591db07496601ebc7a059dd55cfe9
this command is to recover the formal commit using SHA

For more info, [click this url](http://git-scm.com/book/zh/v1/Git-%E5%86%85%E9%83%A8%E5%8E%9F%E7%90%86-%E7%BB%B4%E6%8A%A4%E5%8F%8A%E6%95%B0%E6%8D%AE%E6%81%A2%E5%A4%8D)

###Install jekyll
$ sudo gem update --system
update the gem to latest version
$ sudo gem install jekyll
install jekyll

