---
layout: post
title: Install Latest postgresql using yum from pgsqlrpms
date: 2012-06-25 13:45:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '5500604826637169757'
---
<div dir="ltr" style="text-align:left;">install Latest postgresql using yum from pgsqlrpms<br />##################################################</p>
<p>[root@server ~]# yum erase postgresql postgresql-server<br />[root@server ~]# wget http://yum.pgsqlrpms.org/reporpms/8.3/pgdg-centos-8.3-4.noarch.rpm<br />[root@server ~]# rpm -ivh pgdg-centos-8.3-4.noarch.rpm<br />[root@server ~]# yum install postgresql postgresql-server<br />[root@server ~]# chkconfig postgresql on<br />[root@server ~]# service postgresql initdb<br />[root@server ~]# chkconfig postgresql on &amp;&amp; service postgresql start</p>
<p>[root@server ~]# /usr/bin/postgres --version<br />postgres (PostgreSQL) 8.3.4<br />[root@server ~]#</div>
