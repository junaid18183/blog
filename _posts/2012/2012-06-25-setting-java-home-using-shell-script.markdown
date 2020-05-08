---
layout: post
title: Setting Java Home using shell script
date: 2012-06-25 12:32:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '5937772659047801461'
---
<div dir="ltr" style="text-align:left;">
<div># Use JAVA_HOME if set, otherwise look for java in PATH<br />if [ -x $JAVA_HOME/bin/java ]; then<br />    JAVA=$JAVA_HOME/bin/java<br />else<br />    JAVA=`which java`<br />    export JAVA_HOME=$(readlink -f $JAVA | sed "s:bin/java::")<br />fi</div>
</div>
