---
layout: post
title: SNMP configuration in Linux EC2 for Cacti
date: 2013-07-16 06:57:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '2132693573689721619'
---
<div dir="ltr" style="text-align:left;">1) Install snmpd and snmp</p>
<blockquote class="tr_bq"><p>apt-get install snmpd<br />apt-get install snmp</p></blockquote>
<p>2) Move  original conf file</p>
<blockquote class="tr_bq"><p>mv /etc/snmp/snmpd.conf  /etc/snmp/snmpd.conf.org</p></blockquote>
<p>3) Create new Conf file and add details</p>
<blockquote class="tr_bq"><p>vi /etc/snmp/snmpd.conf</p></blockquote>
<p>add following lines</p>
<blockquote class="tr_bq"><p>rocommunity  me&amp;me<br />syslocation  "AWS"<br />syscontact  junedm@tipsntraps.com</p></blockquote>
<p>4) edit snmpd options, comment SNMODOPTS line and below sample line</p>
<blockquote class="tr_bq"><p>vi /etc/default/snmpd<br /># snmpd options (use syslog, close stdin/out/err).<br />#SNMPDOPTS='-Lsd -Lf /dev/null -u snmp -g snmp -I -smux -p /var/run/snmpd.pid'<br />SNMPDOPTS='-Lsd -Lf /dev/null -u snmp -I -smux -p /var/run/snmpd.pid -c /etc/snmp/snmpd.conf 0.0.0.0'<br />#SNMPDOPTS='-Lsd -Lf /dev/null -u snmp -I -smux -p /var/run/snmpd.pid 0.0.0.0'</p></blockquote>
<p>5) Restart the snmpd service</p>
<blockquote class="tr_bq"><p>/etc/init.d/snmpd restart</p></blockquote>
<p>6) Confirm snmp port is open</p>
<blockquote class="tr_bq"><p>netstat -au | grep snmp<br />netstat -tanpu | grep 161</p></blockquote>
<p>7) Confirm from local machine that you are getting SNMP details</p>
<blockquote class="tr_bq"><p>snmpwalk -v1  -c me&amp;me -O e localhost</p></blockquote>
<p>********************************************</p>
<p>open port 161 in your security Group</p>
<p>and from Cacti machine Run</p>
<p>snmpwalk -v 1 -c me&amp;me -O e 10.32.33.128</p>
<p>#       sec.name     source           community<br />##       ========     ======           =========<br />com2sec  local       localhost        me&amp;me<br />com2sec  GW_MACHINE   10.40.93.211    me&amp;me</p>
<p>##       Access.group.name   sec.model        sec.name<br />##       =================  =========         ========<br />group    MyROGroup_1        v2c               local<br />group    MyROGroup_2        v2c               GW_MACHINE</p>
<p>##   MIB.view.name     incl/excl  MIB.subtree  mask<br />##   ==============   =========  ===========  ====<br />view all-mibs         included   .1           80</p>
<p>##      MIB               <br />##      group.name   context sec.model sec.level prefix read     write  notif<br />##      ==========   ======= ========= ========= ====== ====     =====  =====<br />access  MyROGroup_1  ""       v2c      noauth    exact  all-mibs none   none<br />access  MyROGroup_2  ""       v2c      noauth    exact  all-mibs none   none</p>
<p>###############################</p>
<p>SNMP</p>
<p>OW to activate the SNMP clients</p>
<p>SNMP agents must be only run in Read-Only (RO) mode because the SNMP poller needs only to read data on the remote machines. Limiting how has the right to poll the agents on the remote devices increase a little the security.<br />Never forget that the SNMP community string is going across the network in the clear and can be intercepted easily with tools like WireShark, the former Ethereal.</p>
<p>1. LINUX <span class="Apple-tab-span" style="white-space:pre;">  </span>2. WINDOWS <span class="Apple-tab-span" style="white-space:pre;">  </span>3. CISCO <span class="Apple-tab-span" style="white-space:pre;">  </span>4. NETSCREEN</p>
<p>1. On a debian/Ubuntu Linux machine:</p>
<p>Install the SNMP daemon:</p>
<p>#apt-get install snmpd<br />Configure the SNMP daemon:<br />Edit /etc/snmp/snmpd.conf<br />Comment the "com2sec paranoid default public" line and uncomment the "com2sec readonly default public" line. Don't forget to configure your SNMP community and limit who has the right to poll the SNMP daemon:</p>
<p>#com2sec paranoid default public<br />com2sec readonly snmp_server_ip_address your_snmp_community<br />#com2sec readwrite default private<br />For example:<br />com2sec readonly 10.0.0.1 armageddon<br />Where 10.0.0.1 is the SNMP poller server and armageddon the SNMP read-only community.</p>
<p>Always in the /etc/snmp/snmpd.conf file, you can configure the SNMP syslocation and syscontact settings.<br />Look for the lines beginning with syslocation and syscontact and do your changes:</p>
<p>syslocation Geneva/Switzerland<br />syscontact Roger Rabbit<br />Then restart the SNMP daemon:</p>
<p>/etc/init.d/snmpd restart</p>
<p>References</p>
<p>http://www.it-slav.net/blogs/2009/02/05/install-and-configure-snmp-on-ubuntu/</p>
<p>http://docs.cacti.net/manual:087:2_basics.1_first_graph#my_first_graph</p>
<p>http://www.linuxhomenetworking.com/wiki/index.php/Quick_HOWTO_:_Ch22_:_Monitoring_Server_Performance</p></div>
