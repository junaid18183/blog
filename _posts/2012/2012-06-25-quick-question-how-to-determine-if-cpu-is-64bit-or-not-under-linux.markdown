---
layout: post
title: Quick question, how to determine if CPU is 64bit or not under Linux?
date: 2012-06-25 13:41:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '3956985004492795538'
---
<div dir="ltr" style="text-align:left;">
<div>A. You need to use uname <span class="IL_AD" id="IL_AD12">command<span class="IL_AD_ICON"></span></span>, which prints <span class="IL_AD" id="IL_AD10">system<span class="IL_AD_ICON"></span></span> information including <span class="IL_AD" id="IL_AD11">kernel<span class="IL_AD_ICON"></span></span> version and whether kernel is 32 bit or 64 bit. You can also use less /proc/cpuinfo command determine if it is 64 bit cpu or not.<br />Example - Find out if Running kernel is 32 or 64 bit</p>
<p>$ uname -a<br />Output:</p>
<p>Linux ora100 2.6.5-7.252-smp #1 SMP Tue Feb 14 11:11:04 UTC 2006 x86_64 x86_64 x86_64 GNU/Linux</p>
<p>x86_64 GNU/Linux indicates I have 64bit kernel running. If you use see i386/i486/i586/i686 it is a 32 bit kernel.<br /><span class="IL_AD" id="IL_AD9">How do I<span class="IL_AD_ICON"></span></span> find out CPU is <span class="IL_AD" id="IL_AD3">32bit<span class="IL_AD_ICON"></span></span> or 64bit?</p>
<p>Simply type the following command and if you see lm in output, you have a 64 bit system:<br />$ grep <span class="IL_AD" id="IL_AD5">flags<span class="IL_AD_ICON"></span></span> /proc/cpuinfo<br />Output:</p>
<p>flags            : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca  cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe nx lm  constant_tsc pni monitor ds_cpl vmx est tm2 ssse3 cx16 xtpr lahf_lm</p>
<p>flags            : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca  cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe nx lm  constant_tsc pni monitor ds_cpl vmx est tm2 ssse3 cx16 xtpr lahf_lm<br />flags            : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca  cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe nx lm  constant_tsc pni monitor ds_cpl vmx est tm2 ssse3 cx16 xtpr lahf_lm</p>
<p>flags            : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca  cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe nx lm  constant_tsc pni monitor ds_cpl vmx est tm2 ssse3 cx16 xtpr lahf_lm</p>
<p>    * lm means Long mode - 64 bit CPU<br />    * Real mode 16 bit CPU<br />    * Protected Mode is 32-bit CPU</div>
</div>
