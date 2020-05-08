---
layout: post
title: 'Apache Address already in use: make_sock: could not bind to port 80 error
  and solution'
date: 2012-06-25 12:50:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '545251470616008857'
---
<div dir="ltr" style="text-align:left;">
<div>while configuration for apache , if we get an error like this :-</p>
<p><b><span style="color:blue;">Apache Address already in use: make_sock: could not bind to port 80 error and <span class="IL_AD" id="IL_AD3">solution<span class="IL_AD_ICON"></span></span></span></b></p>
<p>Then chk following service is running ( using port 80 or not)</p>
<p><span style="color:red;"><span style="text-decoration:underline;"><b>tux</b></span></span> enabled (a kernel level web <span class="IL_AD" id="IL_AD6">server<span class="IL_AD_ICON"></span></span>) or something similar , stop that ..</div>
<div></div>
<div></div>
<blockquote class="tr_bq"><p><span>Also you </span><span class="IL_AD" id="IL_AD5">can find<span class="IL_AD_ICON"></span></span><span> all the open files on the port 80 using </span><span class="IL_AD" id="IL_AD4">command<span class="IL_AD_ICON"></span></span></p>
<p><span>lsof -i:80</span></p>
<p><span>then you can kill all those PID then you can restart apache. </span></p></blockquote>
</div>
