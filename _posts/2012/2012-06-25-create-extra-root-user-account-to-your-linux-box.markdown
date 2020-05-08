---
layout: post
title: Create extra root user account to your Linux box.
date: 2012-06-25 14:06:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '5930082400578868247'
---
<div dir="ltr" style="text-align:left;"><span style="text-decoration:underline;"><b>Create extra root user account to your Linux box.</b></span>
<div class="post" id="msg_615">  <br />The ‘root’ <span class="IL_AD" id="IL_AD5">account with<span class="IL_AD_ICON"></span></span> user id 0 is the powerful user account in Linux and Unix system.  You can create <span class="IL_AD" id="IL_AD11">duplicate<span class="IL_AD_ICON"></span></span> root account that have the same <span class="IL_AD" id="IL_AD3">privileges<span class="IL_AD_ICON"></span></span> as root account in the linux.</p>
<p><b>user id for ‘root’:</b> <br />  <br /><tt>[root@server ~]# id root <br />uid=0(root) gid=0(root) groups=0(root),1(bin),2(daemon),3(sys),4(adm),6(disk),10(wheel) </tt><br />  <br /><b>Explanation: </b><br />uid=0(root) <span class="IL_AD" id="IL_AD4">The user<span class="IL_AD_ICON"></span></span> id for user 'root' is 0. <br />gid=0(root) the group id for user ‘root’ is 0. <br />groups=0(root),1(bin),2(daemon),3(sys),4(adm),6(disk),10(wheel) The user ‘root’ is belongs to all above groups.<br />  </p>
<p><tt>[root@server ~]# less /etc/passwd <br />root:x:0:0:root:/root:/bin/bash <br />[root@server ~]# less /etc/shadow <br />root:$1$B2BEWv4X$Gb.QPb6I3RwCkEkz13ow21:13080:0:99999:7::: <br />[root@server ~]# less /etc/group <br />root:x:0:root <br />bin:x:1:root,bin,daemon <br />daemon:x:2:root,bin,daemon <br />sys:x:3:root,bin,adm <br />adm:x:4:root,adm,daemon <br />tdisk:x:6:root <br />wheel:x:10:root </tt><br />  <br />  <br /><b>command: </b><br /><b>  <tt><br />[root@server ~]# adduser -u 0 -o -g 0 -G 0,1,2,3,4,6,10 -M root2 </tt></b><br />  <br />-M: this option creates user without home directory.  </p>
<p>you need <span class="IL_AD" id="IL_AD6">to have<span class="IL_AD_ICON"></span></span> the <span class="IL_AD" id="IL_AD7">administrative<span class="IL_AD_ICON"></span></span> <span class="IL_AD" id="IL_AD2">privilege<span class="IL_AD_ICON"></span></span> on the system in order to issue 'adduser' command above. We can specify  a password for the created user using  “passwd” command.</div>
</div>
