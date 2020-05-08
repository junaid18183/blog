---
layout: post
title: The DVD/CD-ROM drive is not able to be seen in windows explorer
date: 2012-06-26 14:12:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '3583223121083898318'
---
<div dir="ltr" style="text-align:left;">The DVD/CD-ROM drive is not able to be seen in windows explorer. In the device manager, the DVD/CD-ROM drives appear with <span class="IL_AD" id="IL_AD1">exclamation mark<span class="IL_AD_ICON"></span></span>.<br /><b>(Note : for back up Import all registry on ur deskptop )</b><br />   1. On the Windows Start menu, click Run.<br />   2. In the Open box, type Regedit and click OK.<br />   3. Select the following key in the Windows <span class="IL_AD" id="IL_AD6">registry<span class="IL_AD_ICON"></span></span>:<br />   4. HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\<span class="IL_AD" id="IL_AD5">Class<span class="IL_AD_ICON"></span></span>\<br />      {4D36E965-E325-11CE-BFC1-08002BE10318}<br />   5. On the Edit menu, click Delete:<br />      Value Name: LowerFilters<br />      Value Name: UpperFilters<br />   6. On <span class="IL_AD" id="IL_AD3">the Registry<span class="IL_AD_ICON"></span></span> menu, click Exit.<br />   7. Reboot your computer.</p>
<p>Sometimes, you may find only one of the Value Name. You can continue to delete it and restart your computer.</p></div>
