---
layout: post
title: SSH loging without password with RSA key
date: 2012-06-25 14:07:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '4671083247076376328'
---
<div dir="ltr" style="text-align:left;">if you want to automate a backup task to different server and for that  using a bash script one major hurdle is providing password for ssh  session.</p>
<p>to avoid this use RSA keys.</p>
<p>Log in to <span class="IL_AD" id="IL_AD1">Server 1<span class="IL_AD_ICON"></span></span> with your user name  and generate a pair of authentication keys</p>
<div class="quoteheader"></div>
<blockquote class="tr_bq"><div class="quote">[juned@nagios ~]$ ssh-keygen -t rsa<br />Generating public/private rsa key pair.<br />Enter file in which to save the key (/home/juned/.ssh/id_rsa):<br />Enter passphrase (empty for no passphrase):<br />Enter same passphrase again:<br />Your <span class="IL_AD" id="IL_AD8">identification<span class="IL_AD_ICON"></span></span> has been saved in /home/juned/.ssh/id_rsa.<br />Your public key has been saved in /home/juned/.ssh/id_rsa.pub.<br />The key <span class="IL_AD" id="IL_AD4">fingerprint<span class="IL_AD_ICON"></span></span> is:<br />dc:8c:ca:5b:b0:ac:ca:8b:26:f8:3b:cc:73:3e:40:2e <a href="mailto:juned@nagios.rims.com">juned@nagios.rims.com</a></div>
</blockquote>
<p>Now use ssh to create a directory ~/.ssh on <span class="IL_AD" id="IL_AD7">second<span class="IL_AD_ICON"></span></span> server  (The directory may already <span class="IL_AD" id="IL_AD2">exist<span class="IL_AD_ICON"></span></span>, which is fine)</p>
<p>Finally append first servers new public key to second servers .ssh/authorized_keys </p>
<div class="quoteheader"></div>
<blockquote class="tr_bq"><div class="quote">juned@nagios ~]$&gt; cat .ssh/id_rsa.pub | ssh juned@nagios ~]$ 'cat &gt;&gt; .ssh/authorized_keys'</div>
</blockquote>
<p><span class="IL_AD" id="IL_AD3">From now on<span class="IL_AD_ICON"></span></span> you can log in to second server without password </div>
