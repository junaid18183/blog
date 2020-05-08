---
layout: post
title: NRPE plug in resulting wrong output.
date: 2012-06-26 13:35:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '7656685903575141259'
---
<div dir="ltr" style="text-align:left;">Hi I am facing a weird issue. </p>
<p>I have installed NAGIOS and using NRPE plugin for remote <span class="IL_AD" id="IL_AD6">host monitoring<span class="IL_AD_ICON"></span></span>.</p>
<p>I have written a small script <span class="IL_AD" id="IL_AD5">to check<span class="IL_AD_ICON"></span></span> <span class="IL_AD" id="IL_AD2">log files<span class="IL_AD_ICON"></span></span> on remote host , the script is working fine from remote host. but from Nagios server ( NRPE plugin the out put is wrong )</p>
<p>Output from Remote host </p>
<div class="quoteheader"></div>
<div class="quote">
<blockquote class="tr_bq"><b>Server1:/usr/local/nagios/libexec&gt; ./check_batch_status -I air</b><br /><b>OK: Batch is successfully submitted for hour 01</b></p></blockquote>
</div>
<p>NRPE.cfg entry on Remote host</p>
<div class="quoteheader"></div>
<blockquote class="tr_bq"><div class="quote"><b>Server1:/usr/local/nagios/libexec&gt; cat ../etc/nrpe.cfg | grep air<br />command[check_batch_status_air]=/usr/local/nagios/libexec/check_batch_status -I air</b></div>
</blockquote>
<p>Output from Nagios server via NRPE </p>
<div class="quoteheader"></div>
<blockquote class="tr_bq"><div class="quote"><b>-bash-3.1$ ./check_nrpe -H Server1-c check_batch_status_air<br /> CRITICAL:Batch missing for hour 01</b></div>
</blockquote>
<p><a name="more"></a>it was all about due to permission issue.</p>
<p>From host machine I was logged in as a normal user and Nagios server ( NRPE plug in was using Nagios user )</p>
<p>Changing in few permission <span class="IL_AD" id="IL_AD8">structure<span class="IL_AD_ICON"></span></span> solved <span class="IL_AD" id="IL_AD1">the issue<span class="IL_AD_ICON"></span></span>. </div>
