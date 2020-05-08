---
layout: post
title: How to Enable  the Uptime alerts in Check_Mk
date: 2015-05-15 16:31:25.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  _publicize_pending: '1'
---
<p>How to Enable  the Uptime alerts in Check_Mk</p>
<p>&nbsp;</p>
<p>OMD[watchdog]:~/etc/check_mk/conf.d$ cat uptime.mk</p>
<p>check_parameters += [</p>
<p>( {"min": (600, 600)}, ALL_HOSTS, ["Uptime"] ),</p>
<p>]</p>
<p>&nbsp;</p>
