---
layout: post
title: CheckMK memory plugin - Linux free command explained
date: 2015-07-01 07:56:09.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  _publicize_job_id: '12208586087'
---
<p>CheckMK is graphing the numbers on the "-/+ bufferes/cache" line.  This is</p>
<p>a common misconception of the Linux "free" command.</p>
<p>&nbsp;</p>
<p>Linux manages memory by using any unused RAM for disk caching.  The first</p>
<p>time you access a file the kernel will look up the information on your disk</p>
<p>and keep some of that information in RAM.  Your access time to that file</p>
<p>will be slightly faster loading from RAM the next time the file is accessed</p>
<p>and every subsequent time until the cache information is flushed from RAM</p>
<p>(Ex. reboot).  This is the "buffers" and "cached" values on the right side</p>
<p>of the "Mem:" line.</p>
<p>&nbsp;</p>
<p>The RAM that you are thinking about, which is used by programs in user</p>
<p>space (Ex. init,crond,syslog), is on the "-/+ bufferes/cache" line. This</p>
<p>value is 2452 MB which is more in line with the amount of RAM consumed that</p>
<p>you are seeing in your CheckMK graph.  CheckMK is also graphing the used</p>
<p>value on the "Swap:" line in a darker shade of green.</p>
<p>&nbsp;</p>
<p>If you add up the values for "Mem:buffers", "Mem:cached", and "-/+</p>
<p>buffers/cache:used", it should equal close to the number in the "Mem:used"</p>
<p>entry.  This is the total amount of RAM that has been mapped out for usage</p>
<p>by your friendly Linux kernel.</p>
<p>&nbsp;</p>
