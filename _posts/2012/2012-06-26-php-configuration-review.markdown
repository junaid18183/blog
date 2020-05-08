---
layout: post
title: PHP configuration review
date: 2012-06-26 14:00:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '7960859854773131612'
---
<div dir="ltr" style="text-align:left;">often to <span class="IL_AD" id="IL_AD2">check<span class="IL_AD_ICON"></span></span> the PHP configuration setting it is said that review the file php.ino in browser.<br />However you can check the configuration in command line using php -i option.</p>
<p>e.g. to  check what is the path for php.ini file use </p>
<div class="quoteheader"></div>
<blockquote class="tr_bq"><div class="quote">[root@nagios php]# php -i  | grep php.ini<br /><span class="IL_AD" id="IL_AD4">Configuration File<span class="IL_AD_ICON"></span></span> (php.ini) Path =&gt; /usr/local/lib<br /><span class="IL_AD" id="IL_AD1">Loaded<span class="IL_AD_ICON"></span></span> Configuration File =&gt; /usr/local/lib/php.ini</div>
</blockquote>
</div>
