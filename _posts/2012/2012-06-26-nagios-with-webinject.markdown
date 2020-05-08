---
layout: post
title: Nagios with Webinject
date: 2012-06-26 13:47:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '3955633318914063288'
---
<div dir="ltr" style="text-align:left;">I<b><span class="IL_AD" id="IL_AD6">nstall</span> all <span class="IL_AD" id="IL_AD7">Perl</span> packages.</b>
<div class="post" id="msg_1241">
<div class="quoteheader">Quote</div>
<div class="quote">Install "XML::Simple"<br />Install "Crypt::SSLeay"<br />Install "Error" pacakge</div>
<p><b>Install WebInject</b></p>
<div class="quoteheader">Quote</div>
<div class="quote">wget http://<span class="IL_AD" id="IL_AD5">downloads<span class="IL_AD_ICON"></span></span>.sourceforge.net/webinject/webinject-1.41.src.tar.gz</div>
<p><b>ownership </b></p>
<p>change the ownership of web-inject folder </p>
<div class="quoteheader">Quote</div>
<div class="quote">sudo chown nagios:nagios webinject</div>
<p><b>Setup <span class="IL_AD" id="IL_AD1">test cases<span class="IL_AD_ICON"></span></span> in webinject/testcases.xml</b></p>
<p><b>Define a webinject command in /usr/local/nagios/etc/<span class="IL_AD" id="IL_AD2">objects<span class="IL_AD_ICON"></span></span>/commands.cfg</b></p>
<div class="quoteheader">Quote</div>
<div class="quote"># 'webinject' command definition<br />define command {<br />    command_name    webinject<br />    command_line    /usr/local/nagios/webinject/webinject.pl -c $ARG1$ $ARG2$</div>
<p><b>Define a service in /usr/local/nagios/etc/objects/<span class="IL_AD" id="IL_AD3">localhost<span class="IL_AD_ICON"></span></span>.cfg</b></p>
<div class="quoteheader">Quote</div>
<div class="quote">define service {<br />    use                      generic-service<br />    host_name                localhost # Modify<br />    service_description      WebInject test of MyApplication<br />    is_volatile              0<br />    check_period             24x7<br />    max_check_attempts       3<br />    normal_check_interval    1<br />    retry_check_interval     1<br />    contact_groups           admins # Modify<br />    notification_interval    120<br />    notification_period      24x7<br />    notification_options     w,u,c,r<br />    check_command            webinject!config.xml!testcases.xml # Modify<br />}</div>
</div>
</div>
