---
layout: post
title: Difference between Socket and Port
date: 2012-06-26 14:23:00.000000000 +05:30
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
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '3980677440780310221'
---
<div dir="ltr" style="text-align:left;">
<div><span class="IL_AD" id="IL_AD4">Imagine<span class="IL_AD_ICON"></span></span> you computer as a House with many doors. <span class="IL_AD" id="IL_AD1">The address of<span class="IL_AD_ICON"></span></span> your house would be <span class="IL_AD" id="IL_AD8">equal<span class="IL_AD_ICON"></span></span> to the the IP address of a computer. Each door would be equal to a computer's port. A socket would sit at a door and listen and talk. A socket is an a a connection to <span class="IL_AD" id="IL_AD5">another computer<span class="IL_AD_ICON"></span></span>. It would sit at one of your doors and yell across the street to your neighbour's house. In order to do this, <span class="IL_AD" id="IL_AD7">you need to know<span class="IL_AD_ICON"></span></span> what door your neighbour is listening at otherwise he can't answer. You  call up your neighbour and he tells you that he is listening on port  150. You pick a random door at your house with a number above 1024 and  make sure it's empty. If it isn't, you find another one and repeat.(This  is usually handled by the socket and you don't need to specify this.)  Then you open this door and throw a rock to your neighbour's house  across the street and hit the door numbered 150. Your neighbour opens  his door(#150) and you now can talk to him and send him data.</div>
<p><a href="http://www.coderanch.com/t/206360/sockets/java/port-vs-socket"><span>http://www.coderanch.com/t/206360/</span><span class="IL_AD" id="IL_AD6">sockets<span class="IL_AD_ICON"></span></span><span>/java/port-vs-socket</span></a></div>
