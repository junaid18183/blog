---
layout: post
title: Install Sun java JDK 1.5
date: 2012-06-25 13:45:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '8156955863118585112'
---
<div dir="ltr" style="text-align:left;">Install JDK 1.5<br />##################################################</p>
<p>[root@server ~]# cd /root/ &amp;&amp; wget http://72.232.120.3/jdk-1_5_0_15-linux-amd64-rpm.bin<br />[root@server ~]# sh jdk-1_5_0_15-linux-amd64-rpm.bin<br />[root@server ~]# ll /usr/java/jdk1.5.0_15/bin/java<br />[root@server ~]# /usr/sbin/<span class="IL_AD" id="IL_AD4">alternatives<span class="IL_AD_ICON"></span></span> --install /usr/bin/java java /usr/java/jdk1.5.0_15/bin/java 100<br />[root@server ~]# /usr/sbin/alternatives --install /usr/bin/jar jar /usr/java/jdk1.5.0_15/bin/jar 100<br />[root@server ~]# /usr/sbin/alternatives --install /usr/bin/javac javac /usr/java/jdk1.5.0_15/bin/javac 100<br />[root@server ~]# /usr/sbin/alternatives --config java</p>
<p>[root@server ~]# java -version<br />java version "1.5.0_15"<br />Java(TM) 2 Runtime Environment, Standard Edition (build 1.5.0_15-b04)<br />Java <span class="IL_AD" id="IL_AD2">HotSpot<span class="IL_AD_ICON"></span></span>(TM) 64-Bit Server VM (build 1.5.0_15-b04, mixed mode)</p>
<p>[root@server ~]# /usr/bin/postgres --version<br />postgres (PostgreSQL) 8.3.4<br />[root@server ~]#</div>
