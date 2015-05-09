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

      $ git reset --hard 1a410efbd2fdkaldafdkajfdklds059dd55cfe9

this command is to recover the formal commit using SHA

For more info, [click this url](http://git-scm.com/book/zh/v1/Git-%E5%86%85%E9%83%A8%E5%8E%9F%E7%90%86-%E7%BB%B4%E6%8A%A4%E5%8F%8A%E6%95%B0%E6%8D%AE%E6%81%A2%E5%A4%8D)

###Install jekyll
在中国，jekyll所在的网站是被屏蔽的，所以需要用vpn翻墙才能成功执行install jekyll命令x,否则会报超时。

      $ sudo gem update --system

update the gem to latest version

      $ sudo gem install jekyll

install jekyll

if you want to install rails, the command is the same

      $ sudo gem install rails

###jekyll
     
      $ jekyll serve --watch --baseurl ""

this will run the jekyll server, and type the 127.0.0.1:4000 to the url column, you can test or debug the local project

###Google Custom Search Engine(gcse)
First, you need to submit your website and sitemap to google, otherwise, there would be no result. 
[click here to submit google webmasters](https://www.google.com/webmasters/tools/home?hl=en)
Second, customize your google custom search engine API at [here](https://cse.google.com/cse/all)
Finally, If you customize your search engine API and use gcse:searchresults-only featrue,pay attention to the "Query Parameter Name" which has to be given your input name. This problem had costed me half a day to settle down. Otherwise, you can not see any response on the result page after submit your search request. 

###Google Analytics
Click [Google Analytics](http://www.google.com/analytics) to creat your account.

A good way to test if it was well set, click your website url and see the Reporting-->Real-Time-->Overview menu if there would be new sessions and new active pages.


