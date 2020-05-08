---
layout: post
title: Updating glibc on Ubuntu 10.10
date: 2013-09-05 10:53:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- ubuntu
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '7374886930627489213'
---
<div dir="ltr" style="text-align:left;">Recently I was struggling to update the glibc on Ubuntu 10.10 from <span style="background-color:#f7f7f7;font-family:arial, FreeSans, Helvetica, sans-serif;font-size:14px;line-height:20px;">EGLIBC 2.12.</span>  to 2.15</p>
<p>Here are the steps I have taken to perform these tasks</p>
<blockquote class="tr_bq"><p>cd /usr/local/src/</p></blockquote>
<blockquote><p>         wget http://archive.ubuntu.com/ubuntu/pool/main/e/eglibc/eglibc_2.15.orig.tar.gz<br />tar tvzf eglibc_2.15.orig.tar.gz<br />apt-get install alien<br />alien --to-deb eglibc_2.15.orig.tar.gz<br />dpkg -i nscd_2.15-0ubuntu10_amd64.deb libc6_2.15-0ubuntu10_amd64.deb libc6_2.15-0ubuntu10.4_amd64.deb libc-bin_2.15-0ubuntu10.4_amd64.deb</p></blockquote>
<p>and finally reboot :)</p>
<p>And this is how you can confirm</p>
<p>root@:~# aptitude show libc6 | grep Version<br />Version: 2.15-0ubuntu10.4<br />root@:~# aptitude show libc-bin | grep Version<br />Version: 2.15-0ubuntu10.4<br />root@:~# aptitude show nscd | grep Version<br />Version: 2.15-0ubuntu10<br />root@:~# ldd --version | head -n1<br />ldd (Ubuntu EGLIBC 2.15-0ubuntu10.4) 2.15
<div></div>
<p>        </p>
</div>
