---
layout: post
title: how to find total number of mysql slow queries
date: 2012-06-26 14:33:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Mysql
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '375807850021915223'
---
<div dir="ltr" style="text-align:left;">
<div>$mysqladmin -u $User -p password status  2&gt;/dev/null | awk '{print $9}')</div>
</div>
