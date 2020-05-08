---
layout: post
title: Understanding the CPU Usage in Apache server status
date: 2015-08-12 14:08:27.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags:
- Apache
meta:
  _publicize_done_external: a:1:{s:7:"twitter";a:1:{i:12073848;s:57:"https://twitter.com/junaid18183/status/631467292895764485";}}
  _publicize_job_id: '13657222271'
  _publicize_done_12031161: '1'
  _wpas_done_12073848: '1'
  publicize_twitter_user: junaid18183
  publicize_linkedin_url: https://www.linkedin.com/updates?discuss=&scope=99615851&stype=M&topic=6037232987165175808&type=U&a=Ml-d
  _publicize_done_12031166: '1'
  _wpas_done_12073853: '1'
  publicize_google_plus_url: https://plus.google.com/+JunedMemon83/posts/BW7XGFyXTZ2
  _publicize_done_12031176: '1'
  _wpas_done_12073865: '1'
---
<p>I was spending time on graphing the Apache Server status values in graphite ( Cpu load and busy worker etc ) .</p>
<p>While doing all this performance testing I was curious to know about the CPU usage,</p>
<p>So how does the status is saying 2.51% of CPU usage.</p>
<blockquote><p>&lt;dt&gt;Current Time: Wednesday, 12-Aug-2015 06:32:02 PDT&lt;/dt&gt;</p>
<p>&lt;dt&gt;Restart Time: Wednesday, 05-Aug-2015 11:48:40 PDT&lt;/dt&gt;</p>
<p>&lt;dt&gt;Parent Server Generation: 0&lt;/dt&gt;</p>
<p>&lt;dt&gt;Server uptime:  6 days 18 hours 43 minutes 22 seconds&lt;/dt&gt;</p>
<p>&lt;dt&gt;Total accesses: 15410608 - Total Traffic: 104.8 GB&lt;/dt&gt;</p>
<p>&lt;dt&gt;CPU Usage: u14425.6 s284.27 cu0 cs0 - 2.51% CPU load&lt;/dt&gt;</p>
<p>&lt;dt&gt;26.3 requests/sec - 187.5 kB/second - 7.1 kB/request&lt;/dt&gt;</p>
<p>&lt;dt&gt;8 requests currently being processed, 4 idle workers&lt;/dt&gt;</p></blockquote>
<p>So basically the numbers in CPU usage (system and user ) indicate the total cpu time, in seconds, that httpd has been using.</p>
<p>And percentage value is the amount of CPU time used over the existence of the process.</p>
<p>e.g. with above data :</p>
<p>The server is up from 6 days 18 hours 43 minutes 22 seconds i.e. (6*24)*3600+18*3600+43*60+22=585802 seconds</p>
<p>and it has used 14709.87 seconds ( System+user second's ) out of 629002<span style="line-height:1.5;"> i.e. 14709.87/</span>585802<span style="line-height:1.5;">=</span>0.0251  i.e. 2.51%.</p>
<p>On the similar lines the server-status calculates the requests/second.</p>
<p>e.g. with above sample values,</p>
<p>requests_per_second  = Total accesses / uptime in seconds</p>
<p>= 15410608/<span style="line-height:1.5;">585802</span><span style="line-height:1.5;"> = 26.3 </span></p>
<p>Voila, that's how the values are calculated.</p>
<p>So if your server's uptime is quite high  you  will always be getting the cpu usage and throughput averaged out.</p>
<p>And if you are relying too much on CPU Load from server status you will  loose the momentarily load spikes ( so keep watching top too :)</p>
<p>Happy monitoring.</p>
