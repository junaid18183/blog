---
layout: post
title: What is the difference between "su -" and "su" ?
date: 2012-06-25 14:01:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '1322008765125999703'
---
<div dir="ltr" style="text-align:left;">
<div class="post" id="msg_672"><b>What is the difference between "su -" and "su" ?</b> </p>
<p>The main difference between su - and su is that the former makes the <span class="IL_AD" id="IL_AD8">shell<span class="IL_AD_ICON"></span></span> a login shell. This is very important especially if <span class="IL_AD" id="IL_AD2">the user<span class="IL_AD_ICON"></span></span> is going to su from a <span class="IL_AD" id="IL_AD4">regular<span class="IL_AD_ICON"></span></span> <span class="IL_AD" id="IL_AD1">user account<span class="IL_AD_ICON"></span></span> to a root (superuser) account. Normal users do not usually have /sbin/  and /usr/sbin/ in their search path. Therefore if a normal user wants to  execute the command ifconfig, for example, after doing su, he usually  gets the error message:</p>
<p><tt>bash: ifconfig: command not found</tt></p>
<p>With  su -, on the other hand, root's .bashrc and .bash_profile and other  special environment settings get sourced and this puts the sbin  directories into the search path. Below is a sample session:</p>
<p><tt>[testuser@localhost ~]$ su<br />Password:<br />[root@localhost testuser]# <span class="IL_AD" id="IL_AD6">echo<span class="IL_AD_ICON"></span></span> $PATH<br />/usr/kerberos/sbin:/usr/kerberos/bin:/usr/local/bin:/usr/bin:/bin:/usr/X11R6/bin:/home/testuser/bin<br />[root@localhost testuser]# ifconfig<br />bash: ifconfig: command not found<br />[root@localhost testuser]# exit<br />exit<br />[testuser@localhost ~]$ su -<br />Password:<br />[root@localhost ~]# echo $PATH<br />/usr/kerberos/sbin:/usr/kerberos/bin:/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/usr/X11R6/bin:/root/bin<br />[root@localhost ~]# ifconfig<br />eth0 Link encap:<span class="IL_AD" id="IL_AD10">Ethernet<span class="IL_AD_ICON"></span></span> HWaddr 00:A0:CC:39:75:41<br />inet addr:192.168.44.146 Bcast:172.16.45.255 Mask:255.255.254.0<br />inet6 addr: fe80::2a0:ccff:fe39:7541/64 Scope:Link<br />UP BROADCAST RUNNING MULTICAST <span class="IL_AD" id="IL_AD7">MTU<span class="IL_AD_ICON"></span></span>:1500 Metric:1<br />RX packets:21619559 errors:1 dropped:0 overruns:0 frame:87<br />TX packets:21190195 errors:4 dropped:0 overruns:4 carrier:0<br /><span class="IL_AD" id="IL_AD3">collisions<span class="IL_AD_ICON"></span></span>:0 txqueuelen:1000<br />RX bytes:1509569968 (1.4 GiB) TX bytes:2280347397 (2.1 GiB)<br />Interrupt:177 Base address:0x6800</tt></div>
</div>
