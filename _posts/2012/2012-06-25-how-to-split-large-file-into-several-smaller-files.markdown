---
layout: post
title: How to split large file into several smaller files
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
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '709465698988221972'
---
<div dir="ltr" style="text-align:left;">To split large file into several smaller files, you can use split command in linux. Just follow the steps below and you will be able to split large file into smaller files.</p>
<p>    * in your <span class="IL_AD" id="IL_AD5">shell<span class="IL_AD_ICON"></span></span> key in</p>
<p>          $ split –bytes=1m /path/to/large/file<br />          /path/to/output/file/prefix </p>
<p>    * Done. You just split your large file into several smaller files</p>
<p>* You can change the <span class="IL_AD" id="IL_AD1">output file<span class="IL_AD_ICON"></span></span> size by changing the –bytes=1m to your preference. You can use b, k, or  m. b represent bytes, k represent kilobytes, m represent megabytes.</p>
<p>To restore the original file, you can use cat command.<br />To join all the smaller file to restore the original <span class="IL_AD" id="IL_AD2">file type<span class="IL_AD_ICON"></span></span>:-</p>
<p>    $ cat prefix* &gt; NEWFILENAME</p></div>
