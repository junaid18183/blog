---
layout: post
title: securing ps to keep normal users from reading all the processes
date: 2012-06-25 13:40:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '3699278603003015576'
---
<div dir="ltr" style="text-align:left;">
<div>This is one way we secure ps to keep normal users from reading all the processes on the server. <span class="IL_AD" id="IL_AD2">We know<span class="IL_AD_ICON"></span></span> there are other ways to do this and if you would like to share please do.</p>
<p>    *  Moving ps</p>
<p>   1. mv /bin/ps /usr</p>
<p>    * Editing new ps</p>
<p>   1. vi /bin/ps<br />   2. We are creating a <span class="IL_AD" id="IL_AD4">bash<span class="IL_AD_ICON"></span></span> script listed below:</p>
<p>#!/bin/bash</p>
<p>if [ "$(whoami)" != "root" ]; then/usr/ps x</p>
<p>fi</p>
<p>if [ "$(whoami)" = "root" ]; then</p>
<p>/usr/ps $1</p>
<p>fi</p>
<p>    * Allowing ps to run</p>
<p>   1. chmod +x /bin/ps</p>
<p>su - into a normal users login and try and use ps -aux should default and make user ps x</p></div>
</div>
