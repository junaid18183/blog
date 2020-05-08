---
layout: post
title: How to check connections on apache port 80
date: 2012-06-26 12:30:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '2773024931449821476'
---
<div dir="ltr" style="text-align:left;"><b>How to check connections on apache port 80</b></p>
<p>netstat -an |grep :80 |wc –l</p>
<p><b>How to check the last mount time :</b></p>
<blockquote class="tr_bq"><p>root@server [~]#  dumpe2fs  /dev/sdb1 | grep "Last mount time"<br />dumpe2fs 1.39 (29-May-2006)<br />Last mount time:          Tue Sep 22 09:33:36 2009<br />root@server [~]#</p></blockquote>
</div>
