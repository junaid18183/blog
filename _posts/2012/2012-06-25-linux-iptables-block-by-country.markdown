---
layout: post
title: Linux Iptables - Block By Country
date: 2012-06-25 13:33:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '511673466548595777'
---
<div dir="ltr" style="text-align:left;">
<div>I admin a website and a lot of bogus traffic comes from countries that do not offer much in <span class="IL_AD" id="IL_AD1">commercial<span class="IL_AD_ICON"></span></span> value. How do I just configure Apache or iptables to just refuse connections to certain countries?</p>
<p>You  can block traffic at both Apache or iptables level. I recommend  iptables to save some resources. First, you need to get list of  netblocks for each country. Simply visit this page and download IP block  files are provided in CIDR format. Use the following <span class="IL_AD" id="IL_AD5">shell script<span class="IL_AD_ICON"></span></span>:<br />[Warning <span class="IL_AD" id="IL_AD8">examples<span class="IL_AD_ICON"></span></span> may not work!] WARNING!People from other countries may use <span class="IL_AD" id="IL_AD3">proxy<span class="IL_AD_ICON"></span></span> <span class="IL_AD" id="IL_AD4">server<span class="IL_AD_ICON"></span></span> or think of spoofing their <span class="IL_AD" id="IL_AD6">IP address<span class="IL_AD_ICON"></span></span>. In such case, this may not work and it will only protect your box from automated scans or spam.</p>
<p>#!/bin/bash<br />### Block all traffic from AFGHANISTAN (af) and CHINA (CN). Use ISO code ###</p>
<p>ISO="af cn" </p>
<p>### Set PATH ###<br />IPT=/sbin/iptables</p>
<p>WGET=/usr/bin/wget<br />EGREP=/bin/egrep</p>
<p>### No editing below ###<br />SPAMLIST="countrydrop"</p>
<p>ZONEROOT="/root/iptables"<br />DLROOT="http://www.ipdeny.com/ipblocks/data/countries"</p>
<p>cleanOldRules(){</p>
<p>$IPT -F</p>
<p>$IPT -X<br />$IPT -t nat -F<br />$IPT -t nat -X<br />$IPT -t mangle -F</p>
<p>$IPT -t mangle -X<br />$IPT -P INPUT ACCEPT<br />$IPT -P OUTPUT ACCEPT<br />$IPT -P FORWARD ACCEPT</p>
<p>}</p>
<p># create a dir<br />[ ! -d $ZONEROOT ] &amp;&amp; /bin/mkdir -p $ZONEROOT</p>
<p># clean old rules<br />cleanOldRules</p>
<p># create a new iptables list<br />$IPT -N $SPAMLIST</p>
<p>for c  in $ISO<br />do</p>
<p>   # local zone file<br />   tDB=$ZONEROOT/$c.zone</p>
<p>   # get fresh zone file<br />   $WGET -O $tDB $DLROOT/$c.zone</p>
<p>   # country specific log message<br />   SPAMDROPMSG="$c Country Drop"</p>
<p>   # get<br />   BADIPS=$(egrep -v "^#|^$" $tDB)</p>
<p>   for ipblock in $BADIPS<br />   do</p>
<p>      $IPT -A $SPAMLIST -s $ipblock -j LOG --log-prefix "$SPAMDROPMSG"</p>
<p>      $IPT -A $SPAMLIST -s $ipblock -j DROP<br />   done</p>
<p>done</p>
<p># Drop everything<br />$IPT -I INPUT -j $SPAMLIST</p>
<p>$IPT -I OUTPUT -j $SPAMLIST<br />$IPT -I FORWARD -j $SPAMLIST</p>
<p># call your other iptable script<br /># /path/to/other/iptables.sh</p>
<p>exit 0</p>
<p>Save above script as root user and customize ISO variable to <span class="IL_AD" id="IL_AD10">point<span class="IL_AD_ICON"></span></span> out country name using ISO country names. Once done <span class="IL_AD" id="IL_AD9">install<span class="IL_AD_ICON"></span></span> the script as follows using crontab:<br />@weekly /path/to/country.block.iptables.sh<br />To start blocking immediately type:<br /># /path/to/country.block.iptables.sh<br />And you are done with blocking the whole country from your server.<br />iptables geoip patch</p>
<p>Another, <span class="IL_AD" id="IL_AD7">alternative<span class="IL_AD_ICON"></span></span> to above shell script is to use geoip iptables patch. This is not standard iptables modules. You need to download patch and compile Linux kernel.</p>
<p>    * Grab geoipt patch from the <span class="IL_AD" id="IL_AD2">official website<span class="IL_AD_ICON"></span></span>.<br />    * Download and install Linux kernel and iptables <span class="IL_AD" id="IL_AD12">source<span class="IL_AD_ICON"></span></span> code.<br />    * Grab and install tool called patch-o-matic (required for geoip modules).<br />    * Finally, grab GEO IP database from MaxMind. </p>
<p><span class="IL_AD" id="IL_AD11">The details<span class="IL_AD_ICON"></span></span> of kernel compile and iptables patching are beyond the scope of this FAQ. This is left as an exercise to readers. </div>
</div>
