---
layout: post
title: Change the password of root if forgot // Single User Mode without root password
date: 2012-06-25 14:05:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '7300306546511982907'
---
<div dir="ltr" style="text-align:left;">
<table border="0">
<tbody>
<tr>
<td valign="middle"></td>
<td valign="middle"></td>
<td align="right" height="20" style="font-size:smaller;" valign="bottom"></td>
</tr>
</tbody>
</table>
<p><b>Change the password of root if forgot // Single User  Mode without root password for Maintenance </b> </p>
<p><span class="IL_AD" id="IL_AD6">This method<span class="IL_AD_ICON"></span></span> will get you past the "Give root password for maintenance" message, but  the environment will be much more primitive, but this should be enough  for you to issue a 'passwd' command to change the password for root. If  you want to do more than that then you may have to mount filesystems and  <span class="IL_AD" id="IL_AD1">manually<span class="IL_AD_ICON"></span></span> start <span class="IL_AD" id="IL_AD2">the network<span class="IL_AD_ICON"></span></span>. <br />1.   Reboot your machine; press 'Esc' to get to the GRUB menu; select your image; press 'e' to edit; select the Kernel line. <br />2.   Press 'e' to edit the kernel line. Edit <span class="IL_AD" id="IL_AD5">the line<span class="IL_AD_ICON"></span></span> to get rid of quiet and splash; change 'ro' to 'rw'; and add 'init=/bin/bash'. <br />kernel /vmlinuz-2.6.15-27-386 root=/dev/mapper/Ubuntu-root rw init=/bin/bash<br />3.   Press 'enter' then 'b' to boot with these new settings. <br />4.   Change the password ..using passwd command  .</p>
<p><b>Boot into Single User Mode </b> </p>
<p>1.   GRUB:  Boot your Linux box and start hitting 'Esc' until you get the GRUB  menu. The GRUB menu passes by quickly. This can be a <span class="IL_AD" id="IL_AD12">pain<span class="IL_AD_ICON"></span></span> over <span class="IL_AD" id="IL_AD7">VMWare<span class="IL_AD_ICON"></span></span> so you might have to reboot a few times before you catch it. <span class="IL_AD" id="IL_AD9">LILO<span class="IL_AD_ICON"></span></span>: If you are using LILO without no delay set to pause for the boot <span class="IL_AD" id="IL_AD11">prompt<span class="IL_AD_ICON"></span></span> then the process is similar, except that you press and hold any of the  following keys: Shift, Alt, Ctrl, ScrollLock, or CapsLock. <br />2.   Select a boot image from <span class="IL_AD" id="IL_AD4">the menu<span class="IL_AD_ICON"></span></span> <span class="IL_AD" id="IL_AD3">then press<span class="IL_AD_ICON"></span></span> 'e' to edit. <br />3.   Select the Kernel line and press 'e' to edit.  <br />kernel /vmlinuz-2.6.15-27-386 root=/dev/mapper/Ubuntu-root ro quiet splash<br />Edit that line to get rid of quiet and splash and add 'single': <br />kernel /vmlinuz-2.6.15-27-386 root=/dev/mapper/Ubuntu-root ro single<br />Then press enter. You will be returned to the menu. <br />4.   Press 'b' to boot with these new settings. <br />5.   If if appears to boot normally, but you see a message that says: <br />Give root password for maintenance (or type Control-D to continue):</div>
