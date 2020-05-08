---
layout: post
title: GRUB vs. LILO
date: 2012-06-26 12:28:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '2746397556869346352'
---
<div dir="ltr" style="text-align:left;">All boot loaders work in a similar way to fulfill a common purpose. But LILO and GRUB do have a number of <span class="IL_AD" id="IL_AD11">differences<span class="IL_AD_ICON"></span></span>:</p>
<ul style="text-align:left;">
<li>LILO has no interactive command interface, whereas GRUB does.</li>
<li>LILO does not support <span class="IL_AD" id="IL_AD10">booting<span class="IL_AD_ICON"></span></span> from a network, whereas GRUB does.</li>
<li>LILO stores information regarding the location of the operating systems it can to load physically on the   MBR. If you <span class="IL_AD" id="IL_AD2">change your<span class="IL_AD_ICON"></span></span> LILO config file, you have to rewrite the LILO  stage one boot loader to the MBR. Compared with GRUB, this is a much  more risky option since a wrong configured MBR could leave the system  un-bootable. With GRUB, if the <span class="IL_AD" id="IL_AD12">configuration file<span class="IL_AD_ICON"></span></span> is configured incorrectly, it will simply default to the GRUB command-line interface.</li>
<li>GRUB supports MD5 <span class="IL_AD" id="IL_AD8">password protection<span class="IL_AD_ICON"></span></span>, not sure about LILO although  </li>
</ul>
</div>
