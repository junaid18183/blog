---
layout: post
title: Hiding Files Inside An Image in Linux
date: 2012-06-25 13:43:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '6384901294968922761'
---
<div dir="ltr" style="text-align:left;">Here is how to do it in Linux:</p>
<p>Get an image file and an archive of the files that you want to hide. In this example, I have cat beer_and_cig.jpg and hideme.<span class="IL_AD" id="IL_AD1">zip file<span class="IL_AD_ICON"></span></span>. The zip file contains an <span class="IL_AD" id="IL_AD2">MP3 song<span class="IL_AD_ICON"></span></span> that I have stored inside <span class="IL_AD" id="IL_AD3">the archive<span class="IL_AD_ICON"></span></span>. To create the archive-image file, run this <span class="IL_AD" id="IL_AD8">command<span class="IL_AD_ICON"></span></span>:</p>
<p>cat beer_and_cig.jpg hideme.zip &gt; ucantseeme.jpg</p>
<p>What this does is the 'cat' command reads the image file first, then reads the zip file and puts them together in the file named ucantseeme.jpg.</p>
<p>To test the integrity of the image file, try this:</p>
<p># unzip -t ucantseeme.jpg<br />Archive: ucantseeme.jpg<br />warning [ucantseeme.jpg]: 4751 extra bytes at beginning or within zipfile<br />(attempting to process anyway)<br />testing: Feist - 09 - One Two Three Four.mp3 OK<br />No errors detected in compressed data of ucantseeme.jpg.</p>
<p>Notice  the warning message? The test saw that there were few bytes at the  beginning, which means it saw the image file first but the archive is intact and no errors were found.</p>
<p>Perfect!</p></div>
