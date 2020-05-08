---
layout: post
title: Rootsh terminal logger
date: 2012-06-26 12:34:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '6424021282604020534'
---
<div dir="ltr" style="text-align:left;"><b>Rootsh</b> is a shell that logs everything a root user sees on his  terminal. This is useful if you have more than one system administrator  for a server and you want a record of exactly what any given user does.  Despite <span class="IL_AD" id="IL_AD7">the fact<span class="IL_AD_ICON"></span></span> that the latest rootsh release was in March 2005, it still does its job great.</p>
<p><span class="IL_AD" id="IL_AD6">Download<span class="IL_AD_ICON"></span></span> the rootsh <span class="IL_AD" id="IL_AD2">source code<span class="IL_AD_ICON"></span></span> and unpack it in /usr/local folder with a command like tar xvfz  rootsh-1.5.2.tar.gz. At this point you must decide some important things  before you start building the <span class="IL_AD" id="IL_AD11">binaries<span class="IL_AD_ICON"></span></span>. Read the <span class="IL_AD" id="IL_AD12">INSTALL<span class="IL_AD_ICON"></span></span> file in the extracted rootsh folder, where all the choices are documented. I chose to put rootsh's <span class="IL_AD" id="IL_AD4">log files<span class="IL_AD_ICON"></span></span> in the standard place, /var/log, not to log in the syslog file as well, and I don't want system line <span class="IL_AD" id="IL_AD9">numbering<span class="IL_AD_ICON"></span></span> to be written in the log files. At this point you're ready to build the binaries with configure, make, and make install, using arguments to specify the choices you've made:</p>
<blockquote class="tr_bq"><p>~# ./configure --disable-syslog --disable-linenumbering<br />~# make<br />~# make install</p></blockquote>
<p>After you've installed the binaries,  your system is almost ready. You only need to create a rootsh folder  under /var/log/ folder -- mkdir /var/log/rootsh -- in order for rootsh  to be able to put log files there. This <span class="IL_AD" id="IL_AD10">procedure<span class="IL_AD_ICON"></span></span> is not documented, but it's a must.</p>
<p>Suppose  you have three sysadmins who need to administer a specific server. Make  a local user for each, and disable root login thru SSH. Every root user  who logs into the system needs to run the command sudo rootsh in order  for rootsh to start logging. To make life easier, you can put this  command in users' .bash_profile file. Then every time a user logs in,  rootsh will create a new <span class="IL_AD" id="IL_AD3">log file<span class="IL_AD_ICON"></span></span> under /var/log/rootsh. Log file names have the following structure:</p>
<blockquote class="tr_bq"><p><i>..</i></p></blockquote>
<p>e.g, if I list the content of the rootsh folder, I see files like this:</p>
<p>anze.20070424152131.02200.<span class="IL_AD" id="IL_AD8">closed<span class="IL_AD_ICON"></span></span><br />raul.20070424170145.02218.closed<br />pablo.20070425223341.02286.closed<br />pablo.20070425225359.02a9f.closed</p>
<p>The formatting in each log file looks exactly the same as what <span class="IL_AD" id="IL_AD1">the user<span class="IL_AD_ICON"></span></span> sees on his terminal.</div>
