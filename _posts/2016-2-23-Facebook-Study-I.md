---
layout: post
category: [Technology]
title: Facebook Technology Study I
tagline: by Jian
tags: [Facebook, Architecture, Technology]
---

As is known to us all, Facebook is world class big tech company which is engaging in connecting the world with its various open source software and open source hardware. So far Facebook has had 296 open source projects on GitHub with 10+ Million Lines of code, 265k Followers and 43k Forks. This airticle is going to introduce the general open source software infrastructure of Facebook. 
<!--more-->

> Open source is very important for Facebook. Being open is better than being close. Being connection is better than being isolation. Bellow is a short list of facebook's open source software in the last 6 months.


```
grocery-delivery
ig-json-parser
xhp-bootstrap
parseapplinksanalytics
fbcuda
mcrouter
errgroup
third-party
fb-adb
flow
css-layout
httpdown
riftdk1
jsx
vim-flow
flux
dfuse
thpp
immutable-js
fblualib
rpool
osquery
fatal
ds2
proxygen : layer 7 load balancer
fbpca
stats
rebound-js
runcmd
asyncdisplaykit
neti
fbcunn
f8developerconferenceapp
parse-facebook-user-session
parseui-ios
parse-php-sdk
facebook-python-ads-sdk
oss-performance
taste-tester
presto-odbc
between-meals
neti-cookbook
```

Facebook mainly focus on 4 main softwares: data infrastructure like "Presto" and "rocksdb", server runtime like "proxygen" and "HHVM", web framework like "javascript", mobile tools and libraries.

RocksDB is an embeddable persistent key-value store for fast storage. RocksDB can also be the foundation for a client-server database but our current focus is on embedded workloads.

Presto is an open source distributed SQL query engine for running interactive analytic queries against data sources of all sizes ranging from gigabytes to petabytes.

Why open source is very important?

In the year 2004, facebook start with LAMP frame (Linux, Apache, Mysql, PHP),  now it's like a giant LAMP website with third degree scale. Engineers has done a lot to improve the LAMP and memcache.  you had to make it scale. For example, first we use Mysql, then we need to scale it, then need improve it, even replace it. After we release it, we continue using it, it become a loop.

How facebook contribute?

Hardware: Facebook open a hardware project called "open compute project", you can buy those hardware from OEM, they don't have secret anymore.

OCP data center design: mechanical design, electronical design.

---
