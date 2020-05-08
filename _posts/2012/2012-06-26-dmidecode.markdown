---
layout: post
title: dmidecode
date: 2012-06-26 12:29:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '8301906281995529527'
---
<div dir="ltr" style="text-align:left;">The dmidecode command reads the system DMI table to display hardware and BIOS information of the system. This command will <span class="IL_AD" id="IL_AD5">give you<span class="IL_AD_ICON"></span></span> information on the current configuration of your system, as well as the system’s maximum <span class="IL_AD" id="IL_AD3">supported<span class="IL_AD_ICON"></span></span> configuration.</p>
<p>can also use grep with dmidecode <span class="IL_AD" id="IL_AD2">to check<span class="IL_AD_ICON"></span></span> how much RAM my system will support, as follows:</p>
<blockquote class="tr_bq"><p># dmidecode -t memory | grep -i Maximum<br />    Maximum Capacity: 4GB</p></blockquote>
<p>for <span class="IL_AD" id="IL_AD1">more details<span class="IL_AD_ICON"></span></span> check out MAN page.</div>
