---
layout: post
title: Monitoring Hosted website using local nagios instance
date: 2012-06-26 13:44:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '7772848046286311768'
---
<div dir="ltr" style="text-align:left;">Hi, recently I am trying to monitor <span class="IL_AD" id="IL_AD3">the status<span class="IL_AD_ICON"></span></span> of my hosted web page using a local nagios instance.<br />I used nagios check_http plugin for this.</p>
<p>1) Create a new command in <span class="IL_AD" id="IL_AD6">commands<span class="IL_AD_ICON"></span></span>.cfg file and use check_http as your base command and then alter the parameters<br />e.g.</p>
<p>define command{<br />        command_name    check_http_tnt<br />        command_line    $USER1$/check_http -H www.tipsntraps.com $ARG1$<br />        }</p>
<p>2) Define a new service to monitor the web page www.tipsntraps.com/index.php and expect the http_responce code 200</p>
<p>define service{<br />        use                             local-service         ; Name <span class="IL_AD" id="IL_AD2">of service<span class="IL_AD_ICON"></span></span> template to use<br />        host_name                       Rubicon Live<br />        service_description             TNT<br />        check_command                   check_http_tnt! -u /index.php -e 200<br />        notifications_enabled           0<br />        }</p>
<p>3)  Verify the sample Nagios <span class="IL_AD" id="IL_AD5">configuration files<span class="IL_AD_ICON"></span></span>.</p>
<p>/usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg</p>
<p>4) If there are no errors, start Nagios.</p>
<p>/etc/init.d/nagios start</p></div>
