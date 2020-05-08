---
layout: post
title: How can I find hidden processes on my server?
date: 2012-06-25 13:44:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '7207955604985847210'
---
<div dir="ltr" style="text-align:left;">How can I find hidden processes on my server? (linux)</p>
<p>The following line can be used to list out all running processes, regardless of whether or not they show up in 'top'.</p>
<p>mypid=`sysctl kernel.pid_max | cut -d " " -f3`; for rkit in `seq 1 $mypid`; do \<br />test -f /proc/$rkit/cmdline &amp;&amp; (echo -n "[$rkit] "; <span class="IL_AD" id="IL_AD2">strings<span class="IL_AD_ICON"></span></span> /proc/$rkit/cmdline; echo); done</p>
<p>Using this from a shell will <span class="IL_AD" id="IL_AD7">print out<span class="IL_AD_ICON"></span></span> quite a bit of information, so it is suggested that you pipe it to a  file. To do that, you only need to modify the command like so:</p>
<p>mypid=`sysctl kernel.pid_max | cut -d " " -f3`; for rkit in `seq 1 $mypid`; do \<br />test -f /proc/$rkit/cmdline &amp;&amp; (echo -n "[$rkit] "; strings /proc/$rkit/cmdline; echo) &gt;&gt; /root/processes.txt; done</p>
<p>This should allow you to find anything hidden by a root kit, or other users for that matter.  Please note that all of the <span class="IL_AD" id="IL_AD5">previous<span class="IL_AD_ICON"></span></span> goes on one line.  The \ character is there to split <span class="IL_AD" id="IL_AD6">the line<span class="IL_AD_ICON"></span></span> on your screen only, and should be removed if you paste this into an ssh <span class="IL_AD" id="IL_AD8">session<span class="IL_AD_ICON"></span></span>.</div>
