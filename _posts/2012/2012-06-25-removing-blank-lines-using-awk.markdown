---
layout: post
title: removing blank lines using AWK
date: 2012-06-25 12:42:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '7965873423657207825'
---
<div dir="ltr" style="text-align:left;">
<div>cat tvly.log | awk '$0!~/^$/ {print $0}</div>
</div>
