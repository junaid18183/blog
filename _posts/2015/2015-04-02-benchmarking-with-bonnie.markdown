---
layout: post
title: Benchmarking with Bonnie++
date: 2015-04-02 14:54:51.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  _publicize_pending: '1'
  _rest_api_client_id: "-1"
---
<blockquote>yum install http://pkgs.repoforge.org/bonnie++/bonnie++-1.96-1.el6.rf.x86_64.rpm</p>
<p>[root@test~]# rpm -ql bonnie++<br />
/usr/bin/bon_csv2html<br />
/usr/bin/bon_csv2txt<br />
/usr/bin/generate_randfile<br />
/usr/sbin/bonnie++<br />
/usr/sbin/getc_putc<br />
/usr/sbin/getc_putc_helper<br />
/usr/sbin/zcav<br />
/usr/share/doc/bonnie++-1.96<br />
/usr/share/doc/bonnie++-1.96/README.txt<br />
/usr/share/doc/bonnie++-1.96/changelog.txt<br />
/usr/share/doc/bonnie++-1.96/copyright.txt<br />
/usr/share/doc/bonnie++-1.96/credits.txt<br />
/usr/share/doc/bonnie++-1.96/readme.html<br />
/usr/share/man/man1/bon_csv2html.1.gz<br />
/usr/share/man/man1/bon_csv2txt.1.gz<br />
/usr/share/man/man1/generate_randfile.1.gz<br />
/usr/share/man/man8/bonnie++.8.gz<br />
/usr/share/man/man8/getc_putc.8.gz<br />
/usr/share/man/man8/zcav.8.gz</p>
<p>The test File size should be double RAM for good results, RAM is 11900M</p>
<p>[root@test~]# /usr/sbin/bonnie++ -d /tmp -s 24G -n 0 -m TEST -f -b -u prod<br />
Using uid:502, gid:503.<br />
Writing intelligently...done<br />
Rewriting...done<br />
Reading intelligently...done<br />
start 'em...done...done...done...done...done...<br />
Version 1.96 ------Sequential Output------ --Sequential Input- --Random-<br />
Concurrency 1 -Per Chr- --Block-- -Rewrite- -Per Chr- --Block-- --Seeks--<br />
Machine Size K/sec %CP K/sec %CP K/sec %CP K/sec %CP K/sec %CP /sec %CP<br />
TEST 24G 87606 15 55512 7 171794 9 288.1 14<br />
Latency 13726ms 992ms 69113us 151ms</p>
<p>1.96,1.96,TEST,1,1427967244,24G,,,,87606,15,55512,7,,,171794,9,288.1,14,,,,,,,,,,,,,,,,,,,13726ms,992ms,,69113us,151ms,,,,,,</p>
<p>[root@test~]# echo "1.96,1.96,TEST,1,1427967244,24G,,,,87606,15,55512,7,,,171794,9,288.1,14,,,,,,,,,,,,,,,,,,,13726ms,992ms,,69113us,151ms,,,," | bon_csv2html &gt; /tmp/test.html</p></blockquote>
<p><!--more--></p>
<p><a href="https://junaid18183.files.wordpress.com/2015/04/bonnie.png"><img class="alignnone  wp-image-261" src="{{ site.baseurl }}/assets/bonnie.png?w=300" alt="bonnie" width="1200" height="184" /></a><!--more--></p>
