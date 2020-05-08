---
layout: post
title: Restricting Shell Access
date: 2012-06-25 12:29:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '1833361871358040351'
---
<div dir="ltr" style="text-align:left;">By default when you add new user to system (/etc/passwd file) <span class="IL_AD" id="IL_AD1">it grant<span class="IL_AD_ICON"></span></span> shell access, to avoid this for special users for which you dont want to give shell access </p>
<p>add the users with shell option as /sbin/nologin</p>
<p>e.g. to add user Nagios with no shell access:</p>
<div class="quoteheader"></div>
<blockquote class="tr_bq"><div class="quote">useradd -s /sbin/nologin nagios</div>
</blockquote>
<p>to modify already added user with no shell access use </p>
<p>
<div class="quoteheader"></div>
<blockquote class="tr_bq"><div class="quote">usermod -s /sbin/nologin nagios</div>
</blockquote>
<p>By the way /sbin/nologin is <span class="IL_AD" id="IL_AD2">the replacement<span class="IL_AD_ICON"></span></span> for /bin/false method to block <span class="IL_AD" id="IL_AD9">the shell<span class="IL_AD_ICON"></span></span> access.</p>
<p>from http://www.cyberciti.biz site  </p>
<blockquote class="tr_bq"><p>How do I deny access to <span class="IL_AD" id="IL_AD3">user account<span class="IL_AD_ICON"></span></span>? Do I need to use /bin/false or /sbin/nologin to refuse a login?</p>
<p>The /sbin/nologin command politely refuse a login. It <span class="IL_AD" id="IL_AD5">displays<span class="IL_AD_ICON"></span></span> a message that an account is not <span class="IL_AD" id="IL_AD6">available<span class="IL_AD_ICON"></span></span> and exits non-zero. This is prefreed method these days to deny login access to account. You can use it as follows:<br /># usermod -s /sbin/nologin userName</p>
<p>The  /bin/false is old method which does nothing and always return  unsuccessful code. You can use it as follows to deny login access to  existing user:<br /># usermod -s /bin/false userName<br />More About /etc/nologin File</p>
<p>If the file /etc/nologin <span class="IL_AD" id="IL_AD11">exists<span class="IL_AD_ICON"></span></span>,  login will allow access only to root user. ther users will be shown the  contents of this file and their logins will be refused. This is used  when you need to deny login access to all users except root account.  Just create /etc/nologin file and you are done:<br />cat &gt; /etc/nologin</p></blockquote>
</div>
