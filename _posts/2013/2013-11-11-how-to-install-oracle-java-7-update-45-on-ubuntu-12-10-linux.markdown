---
layout: post
title: how-to-install-oracle-java-7-update-45-on-ubuntu-12-10-linux
date: 2013-11-11 08:32:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '7537011066504162849'
---
<div dir="ltr" style="text-align:left;">wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F" http://download.oracle.com/otn-pub/java/jdk/7u45-b18/jdk-7u45-linux-x64.tar.gz<br />tar -xvzf jdk-7u45-linux-x64.tar.gz  -C /usr/lib/jvm<br />cd /usr/lib/jvm<br />ls -ltr<br />update-alternatives --install "/usr/bin/javac" "javac" "/usr/lib/jvm/jdk1.7.0_45/bin/javac" 1<br />update-alternatives --install "/usr/bin/java" "java" "/usr/lib/jvm/jdk1.7.0_45/bin/java" 1<br />update-alternatives --set "javac" "/usr/lib/jvm/jdk1.7.0_45/bin/javac"<br />update-alternatives --set "java" "/usr/lib/jvm/jdk1.7.0_45/bin/java"<br />java -version<br />javac -version</p>
<p>Source :</p>
<p><a href="http://hendrelouw73.wordpress.com/2013/10/16/how-to-install-oracle-java-7-update-45-on-ubuntu-12-10-linux/">http://hendrelouw73.wordpress.com/2013/10/16/how-to-install-oracle-java-7-update-45-on-ubuntu-12-10-linux/</a></div>
