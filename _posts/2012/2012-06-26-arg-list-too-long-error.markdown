---
layout: post
title: Arg list too long error
date: 2012-06-26 12:35:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '7720577291523755190'
---
<div dir="ltr" style="text-align:left;">Most of the time listing on large directory or removing big chunk of files using rm command we face this error <br /><b>arg list too long error </b></p>
<p>Actually this error indicates that we have crossed <span class="IL_AD" id="IL_AD2">the maximum<span class="IL_AD_ICON"></span></span> length of arguments for a process.
<div class="quoteheader"></div>
<blockquote class="tr_bq"><div class="quote">The maximum length of arguments for a new process in Linux is defined by variable called ARG_MAX <span class="IL_AD" id="IL_AD5">to check<span class="IL_AD_ICON"></span></span> the value <br />type the command at the command prompt </p>
<p>juned:/&gt; getconf ARG_MAX<br />131072</div>
</blockquote>
<p>Refer : http://www.in-ulm.de/~mascheck/various/argmax/  for <span class="IL_AD" id="IL_AD1">more details<span class="IL_AD_ICON"></span></span></div>
