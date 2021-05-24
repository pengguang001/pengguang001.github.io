---
layout: post
title: 这两天踩过的坑
---

{{ page.title }}
================

我的AWS lightsail无法访问，那个ip好像被封很长时间了，但amazon每个月收我近4美金，感觉钱花得冤枉。偶然看到腾讯云有一个lighthouse服务，三年298元，感觉挺划算，于是买了一个。

腾讯云很精，给你的只有一个web server，其它wordpress什么的，你需要买它的服务，每月至少几十元。对比来说AWS则很方便，默认把wordpress和mysql什么都给你配好了，用户可以直接上手使用。好吧，省着点儿，自己在lighthouse上安装。偏偏给你的是CentOS，与常用的ubuntu有点差异，用起来需要一直查资料和命令。好不容易把wordpress跑起来了，需要把lightsail上的博客文章转移到lighthouse上，我的思路是在lightsail上用mysqldump把bitnami_wordpress数据库保存到文件，然后导入到lighthouse的数据库。可惜，这样不行，主页显示空白。如果使用空白数据库，则没有问题，wordpress会一步一步提示你进行设置，最终能看到主页。

我希望把域名跟lighthouse ip绑定起来，竟然发现无法访问，提示未备案。进阿里云尝试提交资料备案，结果org域名暂不支持备案。天啊，这样的话我花298买lighthouse有什么用！

折腾累了，想到github有一个主页功能，可是比较简单，灵活性不够。偶然间找到一个jeykll的项目，利用它也能在github上建一个像模像样的主页。找人家的现成的，clone过来，略作修改，还不错。

好吧，我还是想把lightsail上的文章传到github。奇怪的是，lightsail的mysql数据库竟然启动不了，sudo /opt/bitnami/ctlscript.sh显示mysql not running，尝试很多方式，依然启动失败。在aws console上重启实例，也不行（这时我有另一个发现，停止再启动实例，发现公网ip竟然变了，现在竟然能通过web访问，尽管提示数据库连接失败。早点发现这个就好了，省得购买lighthouse）。可是我记得很清楚，前两天mysql还好好的，要不然怎么利用mysqldump来备份数据库呢？

折腾了好一会，终于发现起因，前两天备份数据时产生了一个好几G的大文件（总共20G），导致磁盘占用近99%。把这个文件删掉，重启实例，mysql运行OK。

lightsail要不要停掉呢？这是国外的ip，域名绑定时不需要备案，使用起来很方便。需要再考虑以下。

lighthouse先放着吧，298元买的，不可能退掉了。

github jeykll方案也不错，免费方案。

