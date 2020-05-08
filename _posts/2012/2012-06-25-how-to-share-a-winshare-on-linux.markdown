---
layout: post
title: How to Share a Winshare on Linux:-
date: 2012-06-25 14:02:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '921541411763531984'
---
<div dir="ltr" style="text-align:left;">To mount any windows share/<span class="IL_AD" id="IL_AD3">partition<span class="IL_AD_ICON"></span></span> in Linux use the below command. Here 192.168.3.60 is the IP of <span class="IL_AD" id="IL_AD4">Windows host<span class="IL_AD_ICON"></span></span> and ‘<span class="IL_AD" id="IL_AD2">download<span class="IL_AD_ICON"></span></span>’ is the share name on windows. Then pass on the username of Windows host with password and finally you can mount that share on /mnt in Linux host. <b>Cifs</b> is ‘Common Internet File System’.</p>
<p># mount -t cifs //192.168.3.60/download -o username=guest,password=myPassword  /mnt</div>
