---
layout: post
title: How to add swap space on the linux server?
date: 2012-06-25 14:07:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '8000734162837897004'
---
<div dir="ltr" style="text-align:left;">root@server12:/var/tmp&gt; free -m<br />   total               used       free     shared    buffers     cached<br />Mem:                32186      32024     161          0        248       6086<br />-/+ buffers/cache:25690       6496<br />Swap:               4094       4094          0</p>
<p>root@server12:/var/tmp&gt; dd if=/dev/zero of=/var/tmp/swap/swap0 bs=4096 count=1048576<br />1048576+0 records in<br />1048576+0 records out<br />4294967296 bytes (4.3 GB) copied, 33.6008 seconds, 128 MB/s</p>
<p>root@server12:/var/tmp&gt;  mkswap /var/tmp/swap/swap0<br />Setting up swapspace version 1, size = 4294963 kB</p>
<p>root@server12&gt;  swapon /var/tmp/swap/swap0</p>
<p>root@server12&gt; free -m<br />             total       used       free     shared    buffers     cached<br />Mem:         32186      31942        244          0         99       6225<br />-/+ buffers/cache:     25617       6569<br />Swap:         8190       4094       4095</p>
<p>root@server12&gt; swapon -s<br />Filename                                Type            Size        Used        Priority<br />/dev/sda5                               <span class="IL_AD" id="IL_AD2">partition<span class="IL_AD_ICON"></span></span>       4192924  4192924    -1<br />/var/tmp/swap/swap0                  file           4194296   0             -2<br />root@server12&gt;</div>
