---
layout: post
title: Script to check the Forward/Reverse DNS entries are sane for host
date: 2013-05-02 11:35:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '8655771230012646890'
---
<div dir="ltr" style="text-align:left;">
<blockquote class="tr_bq">
<blockquote class="tr_bq">#! /bin/bash</p></blockquote>
<blockquote class="tr_bq"><p>name=`hostname -f`</p></blockquote>
<blockquote class="tr_bq"><p>ip=$(ifconfig eth0 | grep "inet addr" | awk -F '[: ]' '{print $13}')</p></blockquote>
<blockquote class="tr_bq"><p></p></blockquote>
<blockquote class="tr_bq"><p>forward=$(host $name | awk -F " address " '{print $2}')</p></blockquote>
<blockquote class="tr_bq"><p>reverse=$(host $ip | awk -F "pointer " '{print $2}' | sed 's/\.$//g')</p></blockquote>
<blockquote class="tr_bq"><p></p></blockquote>
<blockquote class="tr_bq"><p></p></blockquote>
<blockquote class="tr_bq"><p>if [ "$ip" = "$forward" ]; then</p></blockquote>
<blockquote class="tr_bq"><p>echo -e "Forward Lookup is ok"</p></blockquote>
<blockquote class="tr_bq"><p>else</p></blockquote>
<blockquote class="tr_bq"><p>echo -e "\nForward lookup does not match with assigned IP address.IP address is $ip while DNS ponits to $forward."</p></blockquote>
<blockquote class="tr_bq"><p>fi</p></blockquote>
<blockquote class="tr_bq"><p></p></blockquote>
<blockquote class="tr_bq"><p>if [ "$name" = "$reverse" ]; then</p></blockquote>
<blockquote class="tr_bq"><p>echo -e "\nReverse Lookup is ok"</p></blockquote>
<blockquote class="tr_bq"><p>else</p></blockquote>
<blockquote class="tr_bq"><p>echo -e "\nReverse lookup does not match with hostname.Hostname is $name while Reverse DNS ponits to $reverse."</p></blockquote>
<blockquote class="tr_bq"><p>fi</p></blockquote>
<div></div>
</blockquote>
</div>
