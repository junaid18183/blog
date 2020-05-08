---
layout: post
title: Installig perl modules
date: 2012-06-26 14:03:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '1209681318617125859'
---
<div dir="ltr" style="text-align:left;">There are several ways to get Perl modules from CPAN installed on your unix-based system.</p>
<p>Before embarking upon any <span class="IL_AD" id="IL_AD11">installation<span class="IL_AD_ICON"></span></span>, it's a good idea to <span class="IL_AD" id="IL_AD2">download<span class="IL_AD_ICON"></span></span> the module, unzip it and <span class="IL_AD" id="IL_AD7">check<span class="IL_AD_ICON"></span></span> out the documentation.<br />The simplest way to get Perl modules installed is to use the CPAN module itself. </p>
<p>If you are the system administrator and want to <span class="IL_AD" id="IL_AD5">install<span class="IL_AD_ICON"></span></span> the module system-wide, you'll need to switch to your root user. To  fire up the CPAN module, just get to your command line and run this: </p>
<p><i>perl -MCPAN -e shell </i></p>
<p>If  this is the first time you've run CPAN, it's going to ask you a series  of questions - in most cases the default answer is fine. <br />Once you find yourself staring at the <i>cpan&gt;</i> command prompt, installing a module is as easy as install MODULE::NAME - for example, to install the HTML::Template module you'd type: </p>
<p><i>cpan&gt; install HTML::Template </i></p>
<p>CPAN should take it from there and you'll wind up with the module installed into your Perl library. <br />Let's say you're on your system command line and you <span class="IL_AD" id="IL_AD12">just want to<span class="IL_AD_ICON"></span></span> install a module as quickly as possible - you can run the Perl CPAN module via command line perl and get it installed in a single line: </p>
<p><i>perl -MCPAN -e 'install HTML::Template' </i></p>
<p>As <span class="IL_AD" id="IL_AD3">mentioned<span class="IL_AD_ICON"></span></span> earlier, it's always advisable to download  a module yourself, especially if you're having problems installing with  CPAN. If you're on the command line, you can use something like wget to  grab the file. Next you'll want to unzip it with something like: </p>
<p><i>tar -zxvf HTML-Template-2.8.tar.gz </i></p>
<p>This will unzip the module into a directory, then you can move in and poke around - look for the README or INSTALL  files. In most cases, installing a module by hand is still pretty easy,  though (although not as easy as CPAN). Once you've switched into the  base directory for the module, you should be able to get it installed by  typing: </p>
<p><i>perl Makefile.PL<br />make<br />make test<br />make install </i></p>
<p><b>Reconfiguring CPAN</b></p>
<p>To alter the CPAN preferences, either edit the Config.pm configuration file <span class="IL_AD" id="IL_AD1">manually<span class="IL_AD_ICON"></span></span>, or use the following command in the CPAN shell.</p>
<p><i>cpan&gt; o conf init</i></p>
<p>The  init configuration option runs through all the configuration questions,  which may be time consuming. For example, other o conf commands can be  used to list, remove, and add mirror sites, and then to save the changes  to disk.</p>
<p><i>cpan&gt; o conf urllist</i><br />urllist<br />ftp://ftp.kernel.org/pub/CPAN/<br />Type 'o conf' to view configuration edit options</p>
<p><i>cpan&gt; o conf urllist shift</i></p>
<p><i>cpan&gt; o conf urllist push ftp://ftp-mirror.internap.com/pub/CPAN/</i></p>
<p><i>cpan&gt; o conf urllist</i><br />urllist<br />ftp://ftp-mirror.internap.com/pub/CPAN/ <br />Type 'o conf' to view configuration edit options</p>
<p><i>cpan&gt; o conf commit</i><br />commit: wrote /usr/local/lib/perl5/5.6.1/CPAN/Config.pm</p>
<p>To manually  edit the existing configuration file, either open the user-specific  ~/.cpan/CPAN/MyConfig.pm directly, or locate the system-wide  configuration file (stored <span class="IL_AD" id="IL_AD4">somewhere<span class="IL_AD_ICON"></span></span> under the perl @INC path list) </p>
<p>Reference:<br />http://sial.org/howto/perl/life-with-cpan/</div>
