---
layout: post
title: Samba permissions-simplified
date: 2012-06-26 12:31:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '5846192412218256287'
---
<div dir="ltr" style="text-align:left;">
<div>Permission precedence</p>
<p>Samba comes with different types of permissions for share. Try to remember few things about UNIX and Samba permissions.<br />(a) <span class="IL_AD" id="IL_AD1">Linux system<span class="IL_AD_ICON"></span></span> permissions take precedence over Samba permissions. For example if a  directory does not have Linux write permission, setting samba writeable =  Yes (see below) will not allow to write to <span class="IL_AD" id="IL_AD8">shared<span class="IL_AD_ICON"></span></span> directory / share.</p>
<p>(b)  The filesystem permission cannot be take priority over Samba  permission. For example if filesystem mounted as readonly setting  writeable = Yes will not allow to write to any shared directory or share via <span class="IL_AD" id="IL_AD7">samba server<span class="IL_AD_ICON"></span></span>.</p>
<p>In short (thanks to Craig [see below in comment section]) :<br />Limits  set by kernel-level access control such as file permissions, file  system mount options, ACLs, and SELinux policies cannot be overridden by  Samba. Both the kernel and Samba must permit <span class="IL_AD" id="IL_AD2">the user<span class="IL_AD_ICON"></span></span> to perform an action on a file before that action can <span class="IL_AD" id="IL_AD6">occur<span class="IL_AD_ICON"></span></span>.</p>
<p>Samba mask permission</p>
<p>It is also possible to specify samba default file creation permission using mask.</p>
<p>    * create mask: This option is set using an octal value when setting permissions for files.<br />    * directory mask: Directories must have the execute bit for proper access. Default parameter is 0755.</div>
</div>
