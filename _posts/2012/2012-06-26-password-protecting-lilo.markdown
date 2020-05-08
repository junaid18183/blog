---
layout: post
title: 'Password Protecting LILO:'
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
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '6566458650592686508'
---
<div dir="ltr" style="text-align:left;">You can <span class="IL_AD" id="IL_AD9">configure<span class="IL_AD_ICON"></span></span> LILO to ask for a password before booting  every operating system or kernel on the system by adding a password  directive in the globally. To do this, open a terminal, log in as root,  and edit /etc/lilo.conf. Before the first image stanza, add a password directive similar <span class="IL_AD" id="IL_AD3">to this<span class="IL_AD_ICON"></span></span>: </p>
<div class="quoteheader"></div>
<blockquote class="tr_bq"><div class="quote">password=password</div>
</blockquote>
<p>In the above directive, replace the word password with your password. </p>
<p>So LILO provide plain text password's compared to GRUB's MD5 password protection</p></div>
