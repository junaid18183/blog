---
layout: post
title: basic postgresql tips
date: 2012-06-26 14:37:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- database
- PostgreSQL
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '1595470164761026054'
---
<div dir="ltr" style="text-align:left;">Start and stop postgresql </p>
<p>Service postgres start </p>
<p>Add to the chkconfig <br />Chkconfig –level 3 postgres on</p>
<p>to create a first user in kubuntu/<span class="IL_AD" id="IL_AD4">ubuntu<span class="IL_AD_ICON"></span></span> linux, type the following:<br />~$ sudo su postgres -c createuser *USERNAME*</p>
<p>Then create a db:<br />~$ sudo su postgres -c createdb *DBNAME*</p>
<p>Then create a password for <span class="IL_AD" id="IL_AD2">the user<span class="IL_AD_ICON"></span></span> by connecting using psql:<br />~$ sudo su postgres -c psql *DBNAME*</p>
<p>Then alter the password:<br />=#ALTER USER *username* WITH PASSWORD ‘*password*‘;<br />=#\q</div>
