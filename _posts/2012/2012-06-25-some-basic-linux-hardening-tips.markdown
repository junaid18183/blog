---
layout: post
title: Some basic Linux Hardening Tips
date: 2012-06-25 12:48:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '18494489846195555'
---
<div dir="ltr" style="text-align:left;">
<div>Few basic things to keep in mind to secure network communications :</p>
<p>1. Remove unneeded <span class="IL_AD" id="IL_AD4">network services<span class="IL_AD_ICON"></span></span>.: R-services such as rlogin, rdist, rexecd, rsh, and rcp are especially vulnerable to hacker attacks.<br />2. Filter access to unknown services in tcpwrappers.<br />3. Filter access using network firewalling rules.<br />4, Do periodic checks to monitor reachability of network services.<br />5.  Controlling File Permissions &amp; Attributes:In Linux, special file  types allow programs to run with the file owner’s rights. SetUID (for  user IDs) and SetGID (for group IDs).Regularly audit <span class="IL_AD" id="IL_AD12">your systems<span class="IL_AD_ICON"></span></span> for any unauthorized and unnecessary use of the setuid or setgid permissions.<br />6. <span class="IL_AD" id="IL_AD9">Manual<span class="IL_AD_ICON"></span></span> testing for Rouge programs:<br />A.Programs that are configured for SetUID:<br />find / -perm -4000 –print<br />B.Programs that are configured for SetGID:<br />find / -perm -2000 –print<br />C.Files that are readable by anyone in the world:<br />find / -perm -2 -type f –print<br />D.Hidden files:<br />find / -name “.*”<br />E.World writable files:<br />root# find / -perm -2 ! -type l –ls<br />F.Files that do not have an owner or belong to no group.<br />root# find / -nouser -o –nogroup</p>
<p>7. Look for Unusual Accounts:<br />Look in /etc/passwd for new accounts in sorted list by UID:<br /># sort –nk3 –t: /etc/passwd | less<br />Normal accounts will be there, but look for new, unexpected accounts, especially with UID &lt; 500.<br />Also, look for unexpected UID 0 accounts:<br /># egrep ':0+:' /etc/passwd<br />On systems that use multiple authentication methods:<br /># getent passwd | egrep ':0+:'<br />Look for orphaned files, which could be a sign of an attacker's temporary account that has been deleted: # find / -nouser –print</p>
<p>8. Look for Unusual Scheduled Tasks<br />Look for cron jobs scheduled by root and any other UID 0 accounts:<br /># <span class="IL_AD" id="IL_AD1">crontab<span class="IL_AD_ICON"></span></span> –u root –l<br />Look for unusual system-wide cron jobs:<br /># cat /etc/crontab<br /># ls /etc/cron.*</p>
<p>====================================================<br /><span class="IL_AD" id="IL_AD10">Automatic<span class="IL_AD_ICON"></span></span> hardening tools to the rescue:</p>
<p>1.Bastille (http://www.bastille-linux.org): an interactive<br />hardening tool. Helps implement a security policy<br />guiding the administrator through different <span class="IL_AD" id="IL_AD7">questions<span class="IL_AD_ICON"></span></span>.<br />Portable and robust.</p>
<p>2.Titan (http://www.fish.com/titan): an automated hardening<br />tool. Implements common <span class="IL_AD" id="IL_AD8">security measures<span class="IL_AD_ICON"></span></span>.<br />====================================================</p>
<p>Security audit tools:</p>
<p>1.Remote <span class="IL_AD" id="IL_AD6">assessment<span class="IL_AD_ICON"></span></span> tools: Nessus, nmap<br />2. Local assessment tools:<br />Some hardening tools can be used: Bastille, Titan<br />Some (H)IDS tools can be used too: Tiger<br />Some other specific tools: LSAT, OVAL</p>
<p>====================================================</p>
<p><span class="IL_AD" id="IL_AD3">Intrusion detection<span class="IL_AD_ICON"></span></span>:<br />Intrusion Detection can be done at different locations:<br />1.Host-based:<br />Kernel audit<br />Integrity analysis of the (file)system<br />Suspicious activities that take place in the host<br />2.Network-based:<br /><span class="IL_AD" id="IL_AD2">Inspection<span class="IL_AD_ICON"></span></span> of packets through <span class="IL_AD" id="IL_AD11">the network<span class="IL_AD_ICON"></span></span> (to any<br />host)<br />Inspection of packets that arrive to the host</p>
<p>====================================================</p>
<p>HIDS tools In user space:</p>
<p>1.Rutinary checks: checksecurity (in different<br />Linux/BSD <span class="IL_AD" id="IL_AD5">distributions<span class="IL_AD_ICON"></span></span>)<br />2.Analysis of logfiles : logcheck,<br />log-analysis,logsnorter<br />3.Filesystem integrity checks (hashes, permissions...):<br />tripwire, aide, integrit samhain, bsign. Can also be<br />done using the package management databases<br />(rpm and dpkg)<br />4.Configuration and security issues: Nabou<br />5.Other: chkrootkit, checkps, adeos, dtk<br />======================================================= </div>
</div>
