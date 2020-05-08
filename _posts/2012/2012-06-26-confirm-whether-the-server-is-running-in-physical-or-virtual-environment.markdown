---
layout: post
title: Confirm whether the server is running in Physical or Virtual environment
date: 2012-06-26 12:56:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '4550559106537991564'
---
<div dir="ltr" style="text-align:left;">Hi guys, </p>
<p>I need to confirm whether my server is running on actual hardware or its under the virtual environment.</p>
<p>Googled it and found few methods </p>
<div class="quoteheader"></div>
<blockquote class="tr_bq"><div class="quote">[root@nagios devices]# lspci | grep <span class="IL_AD" id="IL_AD2">VMware<span class="IL_AD_ICON"></span></span><br />00:0f.0 VGA compatible <span class="IL_AD" id="IL_AD7">controller<span class="IL_AD_ICON"></span></span>: VMware Inc [VMware SVGA II] PCI Display <span class="IL_AD" id="IL_AD5">Adapter<span class="IL_AD_ICON"></span></span></div>
</blockquote>
<p>
<div class="quoteheader"></div>
<blockquote class="tr_bq"><div class="quote">[root@nagios devices]# dmesg |grep  VMware<br />hda: VMware Virtual <span class="IL_AD" id="IL_AD3">IDE Hard Drive<span class="IL_AD_ICON"></span></span>, ATA DISK drive<br />hdc: VMware Virtual IDE CDROM Drive, ATAPI CD/DVD-ROM drive</div>
</blockquote>
<p>but not 100% sure though .... also lspci command needs root <span class="IL_AD" id="IL_AD1">privileges<span class="IL_AD_ICON"></span></span>.</div>
