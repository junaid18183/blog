---
layout: post
title: CentOS 5.2 Local Yum Repository HOWTO
date: 2012-06-25 13:30:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '2159867556955532734'
---
<div dir="ltr" style="text-align:left;">
<div class="post">If you are impatient and want to in have a CentOS 5.2 repository setup so that you don't have to <span class="IL_AD" id="IL_AD12">wait<span class="IL_AD_ICON"></span></span> for each of your systems to download off a CentOS mirror taking up your  time which could be put to better use. Follow the following steps below  and you shouldn't have a problem:</p>
<p>1. <span class="IL_AD" id="IL_AD4">Install<span class="IL_AD_ICON"></span></span> the vsftpd FTP <span class="IL_AD" id="IL_AD2">server<span class="IL_AD_ICON"></span></span>:</p>
<p>yum -y install vsftpd</p>
<p>2. Edit your /etc/vsftpd/vsftpd.conf and change anonymous_enable from NO, to YES and uncomment if necessary.<br />3. Enable the vsftpd service on bootup (System runlevels 2, 3, 4, 5):</p>
<p>/sbin/service vsftpd on</p>
<p>4. Verify you can login to your FTP server anonymously, which will convert a basic directory <span class="IL_AD" id="IL_AD7">listing<span class="IL_AD_ICON"></span></span> to an <span class="IL_AD" id="IL_AD6">index<span class="IL_AD_ICON"></span></span>.html (<span class="IL_AD" id="IL_AD11">quick<span class="IL_AD_ICON"></span></span> and dirty):</p>
<p>wget ftp://localhost/</p>
<p>5. Verify that you have the rsync utility installed, If it not installed install it (yum -y install rsync):</p>
<p>rpm -qa rsync</p>
<p>6. <span class="IL_AD" id="IL_AD5">Locate<span class="IL_AD_ICON"></span></span> user FTP's <span class="IL_AD" id="IL_AD8">home<span class="IL_AD_ICON"></span></span> directory which is the account the anonymous user uses:</p>
<p>echo ~ftp</p>
<p>7. Go to the directory shown:</p>
<p>cd ~ftp</p>
<p>8. Create all of the appropriate directories:</p>
<p>mkdir -pv pub/centos/5.2/{addons,centosplus,extras,fasttrack,os,updates}</p>
<p>9. Create a symbolic link from CentOS 5.2 to 5:</p>
<p>(cd ~ftp/pub/centos &amp;&amp; ln -sf 5.2 5)</p>
<p>10. Go to CentOS Public Mirrors List and find a CentOS mirror which supports RSYNC.</p>
<p>11.  Synchronize with a CentOS mirror now, I don't want SRPMS (Source RPMS),  i386 RPMS or ISOs so you can adjust as necessary, This probably will  take a while depending on what <span class="IL_AD" id="IL_AD1">speed<span class="IL_AD_ICON"></span></span> of connection you are on:</p>
<p>rsync -v -avrt rsync://&lt;rsync server <span class="IL_AD" id="IL_AD10">address<span class="IL_AD_ICON"></span></span> and path to centos 5.2&gt;/ --exclude=SRPMS/ --exclude=i386/ --exclude=*isos* /var/ftp/pub/centos/5.2</p>
<p>12.  Add the command in step 11 after you have verified it works to your  crontab and have it automatically update for you nightly or weekly or  whenver you prefer.</p>
<p>13. While the synchronization is taking place you can create a new CentOS repository file which in the contents put:</p>
<p>[os]<br />name=CentOS-$releasever - OS (Local Repository)<br />baseurl=ftp://server/pub/centos/$releasever/os/$basearch/<br />gpgcheck=0<br />enabled=1</p>
<p>gpgkey=http://mirror.centos.org/centos/RPM-GPG-KEY-CentOS-5</p>
<p>[updates]<br />name=CentOS-$releasever - Updates (Local Repository)<br />baseurl=ftp://server/pub/centos/$releasever/updates/$basearch/</p>
<p>gpgcheck=0</p>
<p>enabled=1<br />gpgkey=http://mirror.centos.org/centos/RPM-GPG-KEY-CentOS-5</p>
<p>[centosplus]<br />name=CentOS-$releasever - Plus (Local Repository)</p>
<p>baseurl=ftp://server/pub/centos/$releasever/centosplus/$basearch/</p>
<p>gpgcheck=0<br />enabled=1<br />gpgkey=http://mirror.centos.org/centos/RPM-GPG-KEY-CentOS-5</p>
<p>[extras]<br />name=CentOS-$releasever - OS (Local Repository)</p>
<p>baseurl=ftp://server/pub/centos/$releasever/extras/$basearch/<br />gpgcheck=0<br />enabled=1<br />gpgkey=http://mirror.centos.org/centos/RPM-GPG-KEY-CentOS-5</p>
<p>[addons]<br />name=CentOS-$releasever - OS (Local Repository)<br />baseurl=ftp://server/pub/centos/$releasever/addons/$basearch/<br />gpgcheck=0</p>
<p>enabled=1</p>
<p>gpgkey=http://mirror.centos.org/centos/RPM-GPG-KEY-CentOS-5</p>
<p>14. Replace the word "server" with the name of your server or <span class="IL_AD" id="IL_AD9">IP address<span class="IL_AD_ICON"></span></span>.</p>
<p>15. Distribute this file to your CentOS <span class="IL_AD" id="IL_AD3">servers<span class="IL_AD_ICON"></span></span> and run the command: yum update, which will update your local yum  databases which track file versioning and locations of packages. On my servers, I also delete the CentOS-Base.repo because I don't need to download files from the CentOS repositories anymore.</div>
</div>
