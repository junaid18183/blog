---
layout: post
title: How to confirm apche has DSO support
date: 2012-06-25 14:11:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '5554391577615463553'
---
<div dir="ltr" style="text-align:left;">To confirm whether your apache was configured with Dynamic Shared Object support <span class="IL_AD" id="IL_AD1">check for<span class="IL_AD_ICON"></span></span> <br /> mod_so.c in your your httpd</p>
<p><span>[root@nagios php]# /usr/local/apache/bin/httpd -l | grep mod_so.c</span><br /><span>  mod_so.c </span></p>
<p>To Find out php <span class="IL_AD" id="IL_AD2">modules<span class="IL_AD_ICON"></span></span> compiled in php use </p>
<blockquote class="tr_bq"><p>php -m</p></blockquote>
</div>
