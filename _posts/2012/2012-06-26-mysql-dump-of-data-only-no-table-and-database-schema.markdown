---
layout: post
title: mysql dump of data only - no table and database schema
date: 2012-06-26 14:44:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- backup
- database
- Mysql
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '8362570593100028970'
---
<div dir="ltr" style="text-align:left;">Mates, I want to dump the data from the tables only rather than its <span class="IL_AD" id="IL_AD4">definition<span class="IL_AD_ICON"></span></span> and data.</p>
<p>The problem with mysqldump is it checks if database/table <span class="IL_AD" id="IL_AD1">exist<span class="IL_AD_ICON"></span></span>  or not. if <span class="IL_AD" id="IL_AD3">the table<span class="IL_AD_ICON"></span></span> exist it drops the table create the blank table and then enters the insert into <span class="IL_AD" id="IL_AD5">statements<span class="IL_AD_ICON"></span></span>. I don't want to use this.</p>
<p><a name="more"></a>goggled and found </p>
<blockquote class="tr_bq"><div class="quote">dump the database with options --no-create-db and --no-create-info</div>
</blockquote>
</div>
