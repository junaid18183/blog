---
layout: post
title: Find command controlling output
date: 2012-06-25 14:04:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '6930481907360265629'
---
<div dir="ltr" style="text-align:left;">Changing the output information<br />If you want more than just the <span class="IL_AD" id="IL_AD3">names of<span class="IL_AD_ICON"></span></span> the files <span class="IL_AD" id="IL_AD1">displayed<span class="IL_AD_ICON"></span></span>, find's -printf action lets you have just about any type of information displayed. Looking at the man page there is a startling array of options.</p>
<p>These are used the most:<br />%p   filename, including name(s) of directory <span class="IL_AD" id="IL_AD5">the file<span class="IL_AD_ICON"></span></span> is in<br />%m   permissions of file, displayed in octal.<br />%f   <span class="IL_AD" id="IL_AD2">displays<span class="IL_AD_ICON"></span></span> the filename, no directory names are included<br />%g   name of the group the file <span class="IL_AD" id="IL_AD6">belongs<span class="IL_AD_ICON"></span></span> to.<br />%h   display name of directory file is in, filename isn't included.<br />%u   username of the owner of the file</p>
<p>As an example:</p>
<div class="quoteheader"></div>
<blockquote class="tr_bq"><div class="quote">find  .  -type d  -printf "%p\t%m\n"</div>
</blockquote>
<p>will print the file name along with permissions </p></div>
