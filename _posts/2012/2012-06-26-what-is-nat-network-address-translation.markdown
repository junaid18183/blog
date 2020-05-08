---
layout: post
title: What is NAT (Network Address Translation)?
date: 2012-06-26 14:26:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Networking
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '4387983217585476025'
---
<div dir="ltr" style="text-align:left;">Network Address Translation (NAT) is an IETF standard that enables a <span class="IL_AD" id="IL_AD5">local area network<span class="IL_AD_ICON"></span></span> (LAN) to use one set of IP <span class="IL_AD" id="IL_AD2">addresses<span class="IL_AD_ICON"></span></span> for internal traffic and a second set of addresses for external traffic. </p>
<p>All necessary IP address translations <span class="IL_AD" id="IL_AD9">occur<span class="IL_AD_ICON"></span></span> where the LAN interfaces with the broader Internet. NAT converts the packet headers (and in some cases the <span class="IL_AD" id="IL_AD4">port numbers<span class="IL_AD_ICON"></span></span> in the headers) for incoming and outgoing traffic and keeps track of each session. <br />This  does mean, however, that NAT overrides "Internet transparency", a  practice in which packets remain intact throughout their transmission.  NAT is also provided with Windows <span class="IL_AD" id="IL_AD1">Internet Connection Sharing<span class="IL_AD_ICON"></span></span>.</p>
<p>NAT accomplishes these key purposes:</p>
<p>•It acts as a firewall by hiding internal IP addresses. <br />•It enables an enterprise to use more internal IP addresses, since there is no possibility of <span class="IL_AD" id="IL_AD3">conflict between<span class="IL_AD_ICON"></span></span> its internal-only IP addresses and those used by other <span class="IL_AD" id="IL_AD8">organizations<span class="IL_AD_ICON"></span></span>. Essentially, an organization can present itself to the Internet with fewer IP addresses than used on its internal network, which conserves public IP addresses. <br />•It allows an enterprise to bundle multiple ISDN connections into one Internet connection. </div>
