---
layout: post
title: Running Jenkins to work with Apache on Port 80
date: 2014-06-23 09:04:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Jenkins
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '3585246544772193443'
---
<div dir="ltr" style="text-align:left;">Tested on Centos 6 and Jenkins installed with RPM from jenkins-1.527-1.1.noarch</p>
<p>Change the /etc/sysconfig/jenkins with right JENKINS_ARGS</p>
<blockquote class="tr_bq"><p>#JENKINS_ARGS="--prefix=/jenkins"  #If you wanna run like http://localhost<br />JENKINS_ARGS=""  # if you wanna run Jenkins on the index </p></blockquote>
<blockquote class="tr_bq"><p>[root@tiber07 jenkins]# cat /etc/httpd/conf.d/jenkins.conf</p>
<p>    ProxyPass         /jenkins  http://localhost:8080/<br />    ProxyPassReverse  /jenkins  http://localhost:8080/<br />    ProxyRequests     Off<br />    ProxyPreserveHost On<br />    <br />        Order deny,allow<br />        Allow from all<br />    <br />    RewriteEngine on<br />    RewriteRule   ^/jenkins/(.+) http://%{HTTP_HOST}/$1</p></blockquote>
<p>#Make sure to change the Proxy Pass location depending what u defined in JENKINS_ARGS</p></div>
