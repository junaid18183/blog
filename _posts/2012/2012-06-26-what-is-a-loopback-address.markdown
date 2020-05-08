---
layout: post
title: What is a loopback address?
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
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '6545934327935148827'
---
<div dir="ltr" style="text-align:left;">This IP address corresponds to the software loopback interface of the <span class="IL_AD" id="IL_AD1">network card<span class="IL_AD_ICON"></span></span>, which does not have hardware associated with it, and does not require a <span class="IL_AD" id="IL_AD10">physical<span class="IL_AD_ICON"></span></span> connection to a network. </p>
<p>The loopback address allows for a reliable method of testing the functionality of an <span class="IL_AD" id="IL_AD3">Ethernet card<span class="IL_AD_ICON"></span></span> and its <span class="IL_AD" id="IL_AD8">drivers<span class="IL_AD_ICON"></span></span> and software without a physical network. It also allows <span class="IL_AD" id="IL_AD11">information technology<span class="IL_AD_ICON"></span></span> professionals to test IP software without worrying about broken or corrupted drivers or hardware. <br />To test a network card  using the loopback address, you can use the TCP/IP utility Ping. The  best way to do this is with the Ping utility that comes with most  operating systems. This is a simple command-line utility that will try  to communicate to an IP address. </p>
<p>Once you are at a command prompt, enter the following:<br />    <i>    ping 127.0.0.1 </i><br />If  the command is successful, the Ping utility will return results similar  to the following. The exact information returned will vary depending on  your operating system:</p>
<p><i>Pinging 127.0.0.1 with 32 bytes of data:<br />Reply from 127.0.0.1: bytes=32 time&lt;10ms TTL=128<br />Ping statistics for 127.0.0.1:<br />Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),<br />Approximate <span class="IL_AD" id="IL_AD5">round<span class="IL_AD_ICON"></span></span> trip times in milli-seconds:<br />Minimum = 0ms, Maximum =  0ms, Average =  0ms </i><br />This indicates that the network card and drivers are functioning properly. If the Ping utility is not able to get a return on the network card, this may indicate either a driver problem, or a physical problem with the <span class="IL_AD" id="IL_AD9">card<span class="IL_AD_ICON"></span></span>. </div>
