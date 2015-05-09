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

###Install jekyll
$ sudo gem update --system
update the gem to latest version
$ sudo gem install jekyll
install jekyll

