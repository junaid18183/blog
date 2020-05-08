---
layout: post
title: How to enable Haproxy Logs in Centos
date: 2015-08-05 11:07:52.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  _edit_last: '52585973'
  geo_public: '0'
  _publicize_job_id: '13425589422'
---
<p>For performance  reasons HAProxy doesn't log directly to files. So we need to handle  that with syslog server.</p>
<p>But Haproxy also requires a syslog to listen on UDP port ( which in default syslog/rsyslog installation is not enabled )</p>
<p>&nbsp;</p>
<p>So  here is how you can enable the Haproxy logging in Centos</p>
<blockquote><p>[root@instance-00000042 haproxy]# cat /etc/rsyslog.d/haproxy.conf<br />
# Enable UDP port 514 to listen to incoming log messages from haproxy<br />
$ModLoad imudp<br />
$UDPServerRun 514<br />
$template Haproxy,"%msg%\n"<br />
local0.=info -/var/log/haproxy/haproxy.log;Haproxy<br />
local0.notice -/var/log/haproxy/admin.log;Haproxy<br />
# don't log anywhere else<br />
local0.* ~</p>
<p>[root@instance-00000042 haproxy]# head /home/prod/lb/conf/GGVA/haproxy/junedtest.1.cfg<br />
global<br />
log 127.0.0.1 local0<br />
log 127.0.0.1 local1 notice<br />
#log loghost local0 info</p></blockquote>
<p>&nbsp;</p>
<p>Restart the rsyslog and you will have your log's ( Make sure to enable the log roation )</p>
<p>&nbsp;</p>
<p>[root@instance-00000042 rsyslog.d]# cd /var/log/haproxy/<br />
[root@instance-00000042 haproxy]# ls -l<br />
total 0<br />
-rw------- 1 root root 0 Aug 5 04:00 admin.log<br />
-rw------- 1 root root 0 Aug 5 04:00 haproxy.log</p>
