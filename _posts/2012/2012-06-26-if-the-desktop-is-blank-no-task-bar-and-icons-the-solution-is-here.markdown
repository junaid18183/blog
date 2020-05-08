---
layout: post
title: If the desktop is blank no task bar and icons ; the solution is here.
date: 2012-06-26 14:10:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '9140187145119495156'
---
<div dir="ltr" style="text-align:left;">On the computer it's not showing the task bar and icons on the desktop, the wallpaper is there the desktop is blank.<br />steps to recover it,</p>
<p>1. Ctrl + Alt + Del to bring up Task Manager.<br />2. Click "New Task..." then click "Browse..."<br />3. Click My Computer on the left panel. Click C:\ - WINDOWS<br />4. Navigate to explorer.exe, right click and copy explorer. Rename it to explorer1 (.exe)<br />5. Hit Cancel to go back to Create New Task window. Type regedit.exe and click OK.<br />6. In the <span class="IL_AD" id="IL_AD1">registry editor<span class="IL_AD_ICON"></span></span>, navigate to the following Key:<br />HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\<span class="IL_AD" id="IL_AD2">Winlogon<span class="IL_AD_ICON"></span></span><br />7. With the Winlogon key selected, look in the right side window for the<br />'<span class="IL_AD" id="IL_AD7">Shell<span class="IL_AD_ICON"></span></span>" value.<br />8. Double click Shell. In the Value Data box, you should see Explorer.exe. Change it to<br />explorer1.exe and click OK.<br />9. Exit the registry editor and reboot the computer </p>
<p>This is caused due to <span class="IL_AD" id="IL_AD3">Trojan virus<span class="IL_AD_ICON"></span></span> after recovering the desktop icons run the antivirus or <span class="IL_AD" id="IL_AD6">malware<span class="IL_AD_ICON"></span></span>.</div>
