---
layout: post
title: strace Wow Much Syscall
date: 2015-08-24 15:20:17.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  _publicize_done_external: a:1:{s:7:"twitter";a:1:{i:12073848;s:57:"https://twitter.com/junaid18183/status/635834023743393792";}}
  _publicize_job_id: '14044947726'
  _publicize_done_12031161: '1'
  _wpas_done_12073848: '1'
  publicize_twitter_user: junaid18183
  publicize_linkedin_url: https://www.linkedin.com/updates?discuss=&scope=99615851&stype=M&topic=6041599718163755008&type=U&a=4M6i
  _publicize_done_12031166: '1'
  _wpas_done_12073853: '1'
  publicize_google_plus_url: https://plus.google.com/+JunedMemon83/posts/HBYX9JE92Cb
  _publicize_done_12031176: '1'
  _wpas_done_12073865: '1'
---
<p>strace is the system call tracer for Linux. It currently uses the arcane ptrace() (process trace) debugging interface, which operates in a violent manner: pausing the target process for each syscall so that the debugger can read state. And doing this twice: when the syscall begins, and when it ends.</p>
<p>This means strace pauses your application twice for each syscall, and context-switches each time between the application and strace. It's like putting traffic metering lights on your application</p>
<p>via <a href="http://www.brendangregg.com/blog/2014-05-11/strace-wow-much-syscall.html">strace Wow Much Syscall</a>.</p>
