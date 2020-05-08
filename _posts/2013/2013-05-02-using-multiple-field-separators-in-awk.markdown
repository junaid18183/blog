---
layout: post
title: Using multiple Field Separators in AWK
date: 2013-05-02 08:29:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '1580406765896412251'
---
<div dir="ltr" style="text-align:left;">Most of the time working with awk we require multiple field separators, e.g. from the o/p of ifconfig you require ip address , BCast address as well netmask you can get all these details in one go as below</p>
<blockquote class="tr_bq"><p>ifconfig eth0 | grep 'inet addr:' | awk -F '[: ]' '{print $13,$16,$19}' </p></blockquote>
<p>Here I am using the white space and colon both as field Separators </div>
