---
layout: post
title: What will happen, if default init level set to 6 in linux?
date: 2012-06-26 12:44:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '6596056100138047757'
---
<div dir="ltr" style="text-align:left;">if  init level set to 6 i.e default run level is 6 . your System keeps  rebooting. To recover from this you need to switch to emergency mode  while machine <span class="IL_AD" id="IL_AD2">boots<span class="IL_AD_ICON"></span></span>. and change the default boot level to 3 or 5 whichever applicable.</p>
<blockquote class="tr_bq"><p>N.B. if the default run level is set to 6 , your system will go upto init.rd and then will jump to reboot without loading <span class="IL_AD" id="IL_AD4">kernel<span class="IL_AD_ICON"></span></span>.</p></blockquote>
</div>
