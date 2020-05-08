---
layout: post
title: Check_MK MRPE
date: 2014-09-11 08:21:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- check_mk
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '6096859797046330214'
---
<div dir="ltr" style="text-align:left;">Check_mk provides a nice way to migrate your old NRPE based checks into Check_mk using <a href="https://mathias-kettner.de/checkmk_mrpe.html">MRPE</a></p>
<p>Although the documentation of MRPE is very comprehensive but today I messed the whole day with small issue.</p>
<p>I had written small script which  can connect to another host by ssh and collect some facts. The problem started when I was using the same command two times with different parameters.</p>
<p>e.g. check my mrpe.cfg</p>
<blockquote class="tr_bq"><blockquote class="tr_bq">[root@appmon2 tmp]# cat  mrpe.cfg</p></blockquote>
<blockquote class="tr_bq"><p>### Just a Test</p></blockquote>
<blockquote class="tr_bq"><p>TEST1 ./test.sh ALL</p></blockquote>
<blockquote class="tr_bq"><p>TEST2 ./test.sh COLO</p></blockquote>
<div></div>
</blockquote>
<p>so despite I have defined two services , check_mk_agent is recongnizing only one,</p>
<blockquote class="tr_bq"><p>[root@tiber tmp]# check_mk_agent</p></blockquote>
<blockquote class="tr_bq"><p>&lt;&lt;&gt;&gt;</p></blockquote>
<blockquote class="tr_bq"><p>(test.sh) TEST1 0 OK: ALL is Green</p></blockquote>
<p>The whole issue was in the script test.sh I have used ssh to connect to remote host and which is causing the issue.</p>
<p>To fix this need to append the </p></div>
<p>[root@tiber tmp]# diff test.sh test1.sh<br />52,53c52<br />&gt; /tmp/juned.txt<br />---<br />&gt;       <br />&gt; /tmp/juned.txt<br />And now check_mk_agent is happy</p>
<blockquote class="tr_bq"><blockquote class="tr_bq">&lt;&lt;&gt;&gt;</p></blockquote>
<blockquote class="tr_bq"><p>(test.sh) TEST1 0 OK: ALL is Green</p></blockquote>
<blockquote class="tr_bq"><p>(test.sh) TEST2 0 OK: app is Green</p></blockquote>
<div></div>
</blockquote>
