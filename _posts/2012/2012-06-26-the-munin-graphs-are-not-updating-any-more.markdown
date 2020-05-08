---
layout: post
title: The Munin graphs are not updating any more
date: 2012-06-26 13:37:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '5568363946206119058'
---
<div dir="ltr" style="text-align:left;">You probably used --force-root with one of the munin programs. You really <span class="IL_AD" id="IL_AD4">shouldn't have<span class="IL_AD_ICON"></span></span> done that. Now fix the ownership of the .rrd <span class="IL_AD" id="IL_AD10">files<span class="IL_AD_ICON"></span></span> and of the .png and .html files so that the munin user can write to them again.</p>
<p>In munin 1.2.6 and 1.3.4 there will be a "<span class="IL_AD" id="IL_AD5">check<span class="IL_AD_ICON"></span></span>-munin" command that checks for correct owner of some files and directories. It does not work well when graph-mode is cgi though.</p>
<p>You can also <span class="IL_AD" id="IL_AD1">check your<span class="IL_AD_ICON"></span></span> configuration, in munin.conf, if you put server's IP, replace it by  127.0.0.1. (example : instead of 88.191.XX.XX, put 127.0.0.1)</p>
<p>Another possibility is that the <span class="IL_AD" id="IL_AD9">structure<span class="IL_AD_ICON"></span></span> of the generated files changed from 1.3.x to 1.4.x. Munin might be updating but the files you are looking av are no longer being updated. A quick fix is to remove all files from the munin-html directory and run munin-update again.</p>
<p>rm -rf /var/www/munin-html/*<br />su -s /bin/<span class="IL_AD" id="IL_AD6">bash<span class="IL_AD_ICON"></span></span> munin<br />/usr/bin/munin-cron</p>
<p>check the Logs of the node using</p>
<p>tail -f /var/log/munin/munin-update.log</p>
<p><a name="more"></a>At any point of time if you update munin configuration (the munin.conf ), update the munin server using munin user only </p>
<p>i.e,. run command </p>
<p>sudo su - munin --shell=/bin/bash </p>
<p>$sudo /usr/share/munin/munin-update </div>
