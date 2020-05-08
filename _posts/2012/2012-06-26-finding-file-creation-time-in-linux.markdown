---
layout: post
title: Finding File Creation Time in Linux
date: 2012-06-26 12:58:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '5320922364862743'
---
<div dir="ltr" style="text-align:left;">The other day I was looking around for <span class="IL_AD" id="IL_AD4">timestamp<span class="IL_AD_ICON"></span></span> at which file is created,</p>
<p>I tried ls -l <br />read stat man pages </p>
<p>and after landed to conclusion that we  can't find creation time for a file. It isn't stored anywhere. </p>
<p>However with ls -l we can find last-modified time <br />and last-accessed time (using "ls -lu") <br />and an inode change time (using  "ls -lc"). </p>
<p>The  latter is often referred to as the "creation time" - even in some man  pages -but that's wrong; it's also set by such operations as mv, ln,  chmod, chown and chgrp.</p></div>
