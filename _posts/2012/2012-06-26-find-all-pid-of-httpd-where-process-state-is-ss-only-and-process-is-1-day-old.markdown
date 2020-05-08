---
layout: post
title: Find all pid of "httpd" where process state is "Ss" only and process is 1 day
  old
date: 2012-06-26 12:54:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '8354381059929042147'
---
<div dir="ltr" style="text-align:left;">We can use etime format that comes with PS command .<br />This option shows the elapsed time since the process was started, in the <span class="IL_AD" id="IL_AD7">the form<span class="IL_AD_ICON"></span></span>: [[dd-]hh:]mm:ss</p>
<p>Now grep the output for finding <span class="IL_AD" id="IL_AD4">processes<span class="IL_AD_ICON"></span></span> with Status Ss and finally you can use AWK/Grep to list all those are  older than 1 day. ( means all output those contains "-" in the out put.</p>
<p>A step <span class="IL_AD" id="IL_AD5">wise<span class="IL_AD_ICON"></span></span> output would be</p>
<blockquote class="tr_bq"><p>[juned@nagios ~]$ ps -A -o pid,user,comm,stat,etime<br />  PID USER     COMMAND          STAT     ELAPSED<br />    1 root     init             S     6-12:06:50<br />    2 root     ksoftirqd/0      SN    6-12:06:50<br />    3 root     events/0         S&lt;    6-12:06:50<br />    4 root     khelper          S&lt;    6-12:06:50<br />31395 root     smbd             S     3-05:44:26<br />32472 apache   httpd            S     2-05:06:13<br /> 2133 root     sshd             Ss      04:03:31<br /> 2135 juned    sshd             S       04:03:28<br /> 2136 juned    <span class="IL_AD" id="IL_AD3">bash<span class="IL_AD_ICON"></span></span>             Ss      04:03:28<br /> 2426 apache   httpd            S          48:18<br /> 2428 apache   httpd            S          48:17<br /> 2429 apache   httpd            S          48:17<br /> 2430 apache   httpd            S          48:17<br /> 2431 apache   httpd            S          48:17<br /> 2721 juned    ps               R+         00:00 </p></blockquote>
<blockquote class="tr_bq"><p>[juned@nagios ~]$ ps -A -o pid,user,comm,stat,etime | grep  httpd<br /> 2356 root     httpd            Ss    6-12:05:39<br /> 2370 apache   httpd            S     6-12:05:38<br /> 2371 apache   httpd            S     6-12:05:38<br /> 2373 apache   httpd            S     6-12:05:38<br /> 2374 apache   httpd            S     6-12:05:38<br />32472 apache   httpd            S     2-05:06:35<br /> 2426 apache   httpd            S          48:40<br /> 2428 apache   httpd            S          48:39<br /> 2429 apache   httpd            S          48:39<br /> 2430 apache   httpd            S          48:39<br /> 2431 apache   httpd            S          48:39 </p></blockquote>
<blockquote class="tr_bq"><p>[juned@nagios ~]$ ps -A -o pid,user,comm,stat,etime | grep Ss |grep  httpd<br /> 2356 root     httpd            Ss    6-12:09:57 </p></blockquote>
<p>
<blockquote class="tr_bq">[juned@nagios ~]$ ps -A -o pid,user,comm,stat,etime | grep Ss |grep  httpd   | awk ' /-/ { print  $1 }'<br />2356 </p></blockquote>
<p>Other way will be :</p>
<p><i><b>ps aux  | grep -w 'Ss' | grep httpd | awk '{print $9,$2}' | sort -t: +1 -9 | grep -v : </b></i></div>
