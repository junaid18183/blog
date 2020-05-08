---
layout: post
title: How to check how much free space we have in Mysql database
date: 2012-06-26 14:39:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- database
- Mysql
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '8711415520368817833'
---
<div dir="ltr" style="text-align:left;">fire the query <br /><i>show table status like 'org';</i></p>
<p>The last column Comments gives the size of the database.</p>
<p><a name="more"></a>If you need to have a <span class="IL_AD" id="IL_AD5">shell script<span class="IL_AD_ICON"></span></span> to check InnoDB_free space of Mysql database here is the code </p>
<p>
<div class="codeheader"></div>
<blockquote class="tr_bq"><div class="codeheader"></div>
<div class="code">
<pre style="display:inline;margin-top:0;">Query="show table status like 'org';"<br />#freespace=${echo "$Query" | mysql -t --host=tiber4 mvc | /bin/awk '/<span class="IL_AD" id="IL_AD3">InnoDB<span class="IL_AD_ICON"></span></span> free:/ {print $38}' }<br />freespace=$(echo "$Query" | mysql -t --host=$host $db | /bin/awk '/InnoDB free:/ {print $38}' )<br /><br />echo $host has $freespace kB free</pre>
</div>
</blockquote>
<p></div>
