---
layout: post
title: Installing ansible on Centos 6
date: 2013-10-31 07:11:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '9015017680382568040'
---
<div dir="ltr" style="text-align:left;">h3. Installing ansible on Centos 6</p>
<p>h5. ansible  dependencies</p>
<p>* python-babel<br />* PyYAML     <br />* python-crypto      <br />* python-jinja2      <br />* python-paramiko <br />* python-simplejson.x86_64 - on all nodes ( if python is lower version than 2.5 )</p>
<p>{code}<br />[root@tiber07vm1 ansible]# ansible --version<br />ansible 1.1<br />{code}</p>
<p>h5. Control Machine (master ) Requirements :</p>
<p>Currently Ansible can be from any machine with Python 2.6 installed</p>
<p>[root@tiber07vm1 download]# python -V<br />Python 2.6.6</p>
<p>h5. Managed Node Requirements<br />On the managed nodes, you only need Python 2.4 or later, but if you are are running less than Python 2.5 on the remotes, you will also need:</p>
<p>h5. Inventory of manged hosts:</p>
<p>Inventory of manged hosts will be at /etc/ansible/hosts</p>
<p>{code}<br />[root@tiber07vm1 ansible]# cat /etc/ansible/hosts<br />[local]<br />tiber07vm1</p>
<p>[remote]<br />tiber07vm3</p>
<p>[all:children]<br />local<br />remote</p>
<p>{code}</p>
<p>h5. First run :</p>
<p>{code}<br />[root@tiber07vm1 ansible]# ansible remote1  -a "uptime" --ask-pass<br />SSH password:<br />tiber07vm4 | success | rc=0 &gt;&gt;<br /> 23:27:18 up 20 days, 11:05,  0 users,  load average: 0.00, 0.00, 0.00</p>
<p>{code}</p>
<p>h5. SSH trust : since you want pass wordless authentication from your master machine ,its advisable to establish a trust</p>
<p>{code}</p>
<p>ssh-copy-id tiber07vm1</p>
<p>ssh-copy-id tiber07vm3</p>
<p>{code}</p>
<p>h5. Sample run :</p>
<p>{code}</p>
<p>[root@tiber07vm1 ansible]# ansible local -a "uptime"<br />tiber07vm1 | success | rc=0 &gt;&gt;<br /> 23:32:56 up 20 days, 11:10,  1 user,  load average: 0.04, 0.02, 0.00</p>
<p>[root@tiber07vm1 ansible]# ansible remote  -a "uptime"<br />tiber07vm3 | success | rc=0 &gt;&gt;<br /> 23:33:01 up 20 days, 11:10,  0 users,  load average: 0.04, 0.02, 0.00</p>
<p>[root@tiber07vm1 ansible]# ansible all -a "uptime"<br />tiber07vm1 | success | rc=0 &gt;&gt;<br /> 23:33:06 up 20 days, 11:11,  1 user,  load average: 0.03, 0.02, 0.00</p>
<p>tiber07vm3 | success | rc=0 &gt;&gt;<br /> 23:33:07 up 20 days, 11:11,  0 users,  load average: 0.03, 0.02, 0.00</p>
<p>{code}
<div></div>
</div>
