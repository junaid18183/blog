---
layout: post
title: Recover/Reset MySQL root Password
date: 2012-06-26 14:31:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Administration
- Mysql
- Password
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '3623904671050244886'
---
<div dir="ltr" style="text-align:left;">Step # 1 : Stop mysql service</p>
<p># /etc/init.d/mysql stop<br />Output:</p>
<p>Stopping <span class="IL_AD" id="IL_AD1">MySQL database<span class="IL_AD_ICON"></span></span> <span class="IL_AD" id="IL_AD8">server<span class="IL_AD_ICON"></span></span>: mysqld.</p>
<p>Step # 2: Start to <span class="IL_AD" id="IL_AD2">MySQL server<span class="IL_AD_ICON"></span></span> w/o password:</p>
<p># mysqld_safe --skip-grant-tables &amp;<br />Output:</p>
<p>[1] 5988<br />Starting mysqld daemon with databases from /var/lib/mysql<br />mysqld_safe[6025]: started</p>
<p>Step # 3: <span class="IL_AD" id="IL_AD7">Connect<span class="IL_AD_ICON"></span></span> to mysql server using mysql client:</p>
<p># mysql -u root<br />Output:</p>
<p>Welcome to the MySQL monitor.  Commands end with ; or \g.<br />Your MySQL connection id is 1 to server version: 4.1.15-Debian_1-log</p>
<p>Type 'help;' or '\h' <span class="IL_AD" id="IL_AD5">for help<span class="IL_AD_ICON"></span></span>. Type '\c' to clear the buffer.</p>
<p>mysql&gt;</p>
<p>Step # 4: Setup new MySQL root user password</p>
<p>mysql&gt; use mysql;<br />mysql&gt; update user set password=PASSWORD("NEW-ROOT-PASSWORD") where User='root';<br />mysql&gt; flush <span class="IL_AD" id="IL_AD3">privileges<span class="IL_AD_ICON"></span></span>;<br />mysql&gt; quit<br />Step # 5: Stop MySQL Server:</p>
<p># /etc/init.d/mysql stop<br />Output:</p>
<p>Stopping MySQL database server: mysqld<br />STOPPING server from pid file /var/run/mysqld/mysqld.pid<br />mysqld_safe[6186]: ended</p>
<p>[1]+  Done                    mysqld_safe --skip-grant-tables</p>
<p>Step # 6: Start MySQL server and test it</p>
<p># /etc/init.d/mysql start<br /># mysql -u root -p</div>
