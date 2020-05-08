---
layout: post
title: Forgot root password? Change root password for Linux in runlevel 1.
date: 2012-06-26 12:55:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '3490426850123222278'
---
<div dir="ltr" style="text-align:left;"><b>Forgot root password? Change root password for Linux using runlevel 1.</b></p>
<p>If  you are unable to remind your root password, then you have to boot your  Linux machine and enter the runlevel 1 for single user mode, <span class="IL_AD" id="IL_AD7">you can do this<span class="IL_AD_ICON"></span></span> using below steps:</p>
<p>1. Power on your Linux Machine. You will get the grub screen.</p>
<p>2. When the GRUB screen appear, press any key on the keyboard, You will get the <span class="IL_AD" id="IL_AD4">operating system<span class="IL_AD_ICON"></span></span> list installed on your system.</p>
<p>3. Then Select the (operating system  - may be linux or fedora or etc..)option that you want to change the  root password using the ‘up’ + ‘down’ arrow keys. Press ‘e” key to edit  the boot command.</p>
<p>4. It will display <span class="IL_AD" id="IL_AD10">selected<span class="IL_AD_ICON"></span></span> kernel - grub. Again use the up + <span class="IL_AD" id="IL_AD8">down arrow<span class="IL_AD_ICON"></span></span> keys to highlight the kernel (e.g kernel /vmlinuz-2.6.18-1.2798.fc6 ro root=/dev/VolGroup00/LogVol00 rhgb <span class="IL_AD" id="IL_AD9">quiet<span class="IL_AD_ICON"></span></span> ) <span class="IL_AD" id="IL_AD3">then press<span class="IL_AD_ICON"></span></span> “e” key to enter the GRUB edit mode. You will get the <span class="IL_AD" id="IL_AD2">linux system<span class="IL_AD_ICON"></span></span> in whatever the runlevel you want.</p>
<p>5. Add the runlevel <span class="IL_AD" id="IL_AD12">number<span class="IL_AD_ICON"></span></span> that you want to boot into, the example below show that we add number “1” at the of that line to boot up Linux operating system using runlevel 1 for single user mode. (e.g kernel /vmlinuz-2.6.18-1.2798.fc6 ro root=/dev/VolGroup00/LogVol00 rhgb quiet 1 )</p>
<p><b>you can use:</b></p>
<p><tt> 1</p>
<p> S</p>
<p>or</p>
<p> single</tt></p>
<p>6. Then press ‘Enter’ key <span class="IL_AD" id="IL_AD1">to apply<span class="IL_AD_ICON"></span></span> the changes and exit the GRUB edit screen.</p>
<p>7. Then press the “b” key to start the boot up process of Linux system in the runlevel 1 mode. (single user mode)</p>
<p>8. After completing the boot up process in runlevel 1, the linux operating system installed on your system <span class="IL_AD" id="IL_AD6">give you<span class="IL_AD_ICON"></span></span> the shell screen that ready to be use…. Notice that hash sign ( # ) on  the screen… this usually indicate that the current user is root user.</p>
<p>9. To change the password for root; use the Linux ‘passwd’ command, see example below:</p>
<p><tt># passwd    [Type in 'passwd' command and hit Enter key]</tt><br /><tt>Changing password for user root.<br />New UNIX password:<br />BAD PASSWORD: it is too simplistic/systematic<br />Retype new UNIX password:</tt><br /><tt><br />passwd: all authentication tokens updated successfully.</tt></p>
<p><tt>sh-3.1# reboot      [&lt;-- Type in &#039;reboot&#039; command and hit Enter key to start reboot your PC]</tt></p>
<p>10. Then after the reboot process <span class="IL_AD" id="IL_AD11">complete<span class="IL_AD_ICON"></span></span>, login to your Linux system and use the new root password you have specified.</p>
<p><span style="text-decoration:underline;"><b>Note:</b></span> if something like passwd: Authentication token lock busy message display on the screen execute command below:</p>
<p><tt>sh-3.1# mount -o remount, rw /    [Then hit the Enter key]</tt></p>
<p>and then execute the password command again:</p>
<p><tt>sh-3.1# passwd   </tt></p>
<p>Congrats!! password for your linux system has been reset.</p></div>
