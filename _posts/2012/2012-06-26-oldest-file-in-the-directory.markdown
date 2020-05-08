---
layout: post
title: Oldest file in the Directory
date: 2012-06-26 12:26:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '6885564153288058222'
---
<div dir="ltr" style="text-align:left;">If you need to find the oldest file in the directory you can use a <span class="IL_AD" id="IL_AD6">shortcut<span class="IL_AD_ICON"></span></span> as </p>
<div class="quoteheader"></div>
<blockquote class="tr_bq"><div class="quote"><span class="IL_AD" id="IL_AD1">Localhost<span class="IL_AD_ICON"></span></span>&gt; ls -t |tail -1<br />20100228-235312-9267-1.pdf</div>
</blockquote>
<p>-t switch Sort by the <span class="IL_AD" id="IL_AD3">timestamp<span class="IL_AD_ICON"></span></span> shown and tail gives you the last line. so you are able to see the oldest file.</p>
<p>To see newest file use </p>
<div class="quoteheader"></div>
<blockquote class="tr_bq"><div class="quote">Localhost&gt; ls -t |head -1<br />20100228-235312-9267-1.pdf</div>
</blockquote>
<p>if you are willing to see long listing change the head -2 ( since long listing creates a summery line at the top of output )</div>
