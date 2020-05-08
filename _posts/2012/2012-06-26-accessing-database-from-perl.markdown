---
layout: post
title: accessing database (from perl).
date: 2012-06-26 08:02:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '3335289986481963469'
---
<div dir="ltr" style="text-align:left;">
<div class="MsoNormal"><span style="font-size:10pt;">#!\usr\bin\perl</span><br /><span style="font-size:10pt;">#selectstar.plx</span></p>
<p><span style="font-size:10pt;">use warnings;</span><br /><span style="font-size:10pt;">use strict;</span></p>
<p><span style="font-size:10pt;">my $res=`echo "select * from checkin;" |mysql -u juned -p -D RNS_database -t `; print "$res";</span></div>
</div>
