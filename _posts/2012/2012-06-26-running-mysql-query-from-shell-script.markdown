---
layout: post
title: Running mysql query from shell script
date: 2012-06-26 14:35:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Mysql
- Shell Script
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '7107927532582998787'
---
<div dir="ltr" style="text-align:left;">This is the simple method to run a mysql query from <span class="IL_AD" id="IL_AD4">Bash<span class="IL_AD_ICON"></span></span> script</p>
<blockquote class="tr_bq"><p>Query3="select * from ta_lookup where gds = 'wsp' and server like  'reported%';"<br /><span class="IL_AD" id="IL_AD3">echo<span class="IL_AD_ICON"></span></span>   "$Query3" | mysql --host=tiber12 mvc </p></blockquote>
<p> ###### mvc is name of database and --host is the database host </div>
