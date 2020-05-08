---
layout: post
title: How do I remove a file with funny characters or space in the filename
date: 2012-06-25 12:45:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '6440706120146087940'
---
<div dir="ltr" style="text-align:left;">
<div>If you can't delete <span class="IL_AD" id="IL_AD1">regular<span class="IL_AD_ICON"></span></span> file with funny characters or space in the filename, then you can delete it using Inode Number.</p>
<p>find . -inum  -exec rm -i {} \;</div>
<div></div>
<p><span>you </span><span class="IL_AD" id="IL_AD4">can find<span class="IL_AD_ICON"></span></span><span> the inode number using </span><span class="IL_AD" id="IL_AD5">command<span class="IL_AD_ICON"></span></span><span>.</span></p>
<p><span>ls -i  </span></div>
