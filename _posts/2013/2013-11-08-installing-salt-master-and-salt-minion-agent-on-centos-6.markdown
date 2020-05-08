---
layout: post
title: Installing salt master and salt minion (agent) on CentOS 6
date: 2013-11-08 05:38:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '7035006936300952658'
---
<div dir="ltr" style="text-align:left;">h3. Installing salt master and salt minion (agent) on CentOS 6</p>
<p>{color:#313131}Beginning with version 0.9.4, Salt has been available in{color}{color:#313131}&nbsp;{color}[EPEL|http://fedoraproject.org/wiki/EPEL]{color:#313131}. It is installable using yum. Salt should work properly with all mainstream derivatives of RHEL, including CentOS.{color}</p>
<p>Salt and all dependencies have been accepted into the yum repositories for EPEL5 and EPEL6. The latest salt version can be found in epel-testing, while an older but more tested version can be found in regular epel.</p>
<p>h5. Salt (master) dependencies:</p>
<p>* PyYAML<br />* libyaml<br />* m2crypto<br />* openpgm<br />* sshpass<br />* python-babel<br />* python-crypto<br />* python-jinja2<br />* python-msgpack<br />* python-zmq<br />* zeromq3</p>
<p>Now installing salt-master.</p>
<p>{code}<br />[root@tiber07vm2 ~]# yum install salt-master</p>
<p>[root@tiber07vm2 ~]# salt --version<br />salt 0.16.4<br />{code}</p>
<p>Install python pip to install python additional modules<br />{code}<br />[root@tiber07vm2 ~]# yum install python-setuptools</p>
<p>[root@tiber07vm2 ~]# easy_install pip<br />{code}</p>
<p>Upgrade salt which is supported version salt-ssh (first resolved the dependancies for it)<br />{code}<br />[root@tiber07vm2 ~]# pip install markupsafe</p>
<p>[root@tiber07vm2 ~]# pip install --upgrade salt</p>
<p>[root@tiber07vm2 ~]# salt --version<br />salt 0.17.1</p>
<p>[root@tiber07vm2 ~]# salt-ssh --version<br />salt-ssh 0.17.1<br />{code}</p>
<p>h5. Basically salt-stack comes with two environment</p>
<p>* Stack master (Server) \-&gt; stack minion (Agent)</p>
<p>* Stack master (SSH) \-&gt; Master connects to agent using ssh, so no additional salt agent is required.</p>
<p>h5. Managed Node Requirements</p>
<p>h5. 1) Salt (minion) dependencies:</p>
<p>On the managed nodes, you only need Python 2.4 or later,<br />* m2crypto<br />* openpgm<br />* python-babel<br />* python-crypto<br />* python-jinja2<br />* python-msgpack<br />* python-yaml&nbsp;&nbsp;<br />* python-zmq&nbsp;&nbsp;&nbsp;&nbsp;<br />* zeromq3&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</p>
<p>Now installing salt-minion.</p>
<p>{code}<br />[root@tiber07vm2 ~]# yum install salt-minion</p>
<p>[root@tiber07vm2 ~]# salt-minion --version<br />salt-minion 0.16.4<br />{code}</p>
<p>h5. Inventory of manged hosts:</p>
<p>Edit the /etc/salt/minion file on salt-minion server and add entry for salt-master server</p>
<p>{code}<br />[root@tiber07vm4 ~]# cat /etc/salt/minion<br />master: tiber07vm2.glam.colo<br />{code}</p>
<p>Start the master and minion services on salt master and client server<br />{code}<br />[root@tiber07vm2 ~]# /etc/init.d/salt-master start<br />Starting salt-master daemon:                               [  OK  ]</p>
<p>[root@tiber07vm2 ~]# /etc/init.d/salt-minion start<br />Starting salt-minion daemon:                               [  OK  ]</p>
<p>[root@tiber07vm4 ~]# /etc/init.d/salt-minion start<br />Starting salt-minion daemon:                               [  OK  ]<br />{code}</p>
<p>Check discovery for new minion and view the certificate requests on master:<br />{code}<br />[root@tiber07vm2 ~]# salt-key -L<br />Accepted Keys:<br />Unaccepted Keys:<br />tiber07vm2<br />tiber07vm4<br />Rejected Keys:<br />{code}</p>
<p>Looks perfect now\!\!</p>
<p>Accept the certificate requests on master:<br />{code}<br />[root@tiber07vm2 ~]# salt-key -A<br />The following keys are going to be accepted:<br />Unaccepted Keys:<br />tiber07vm2<br />tiber07vm4<br />Proceed? [n/Y] Y<br />Key for minion tiber07vm2 accepted.<br />Key for minion tiber07vm4 accepted.<br />{code}</p>
<p>Verify to see keys are accepted<br />{code}<br />[root@tiber07vm2 ~]# salt-key -L<br />Accepted Keys:<br />tiber07vm2<br />tiber07vm4<br />Unaccepted Keys:<br />Rejected Keys:<br />{code}</p>
<p>h5. Test the connection with the children:</p>
<p>Great you have done so far, now it is time to test</p>
<p>{code}<br />[root@tiber07vm2 ~]# salt 'tiber07vm4' test.ping<br />tiber07vm4:<br />    True</p>
<p>[root@tiber07vm2 ~]#  salt '*' test.ping<br />tiber07vm4:<br />    True<br />tiber07vm2:<br />    True<br />{code}</p>
<p>h5. 2) Salt (ssh) dependencies:</p>
<p>On the managed nodes, you only need Python 2.4 or later.</p>
<p>h5. SSH trust : since you want pass wordless authentication from your master machine ,its advisable to establish a trust</p>
<p>{code}<br />ssh-copy-id tiber07vm2</p>
<p>ssh-copy-id tiber07vm4<br />{code}</p>
<p>Inventory of manged hosts will be at /etc/salt/roster, this example configuration contains host without password (shared auth_key) and with password host entries.<br />{code}<br />[root@tiber07vm2 ~]# cat /etc/salt/roster<br />tiber07vm2:<br />  host: tiber07vm2<br />  user: root<br />tiber07vm4:<br />  host: tiber07vm4<br />  user: root<br />  passwd: myrootpassword<br />{code}</p>
<p>h5. Test the connection with the children:</p>
<p>Great you have done all, now it is time to test</p>
<p>{code}<br />[root@tiber07vm2 ~]# salt-ssh '*' test.ping<br />tiber07vm2:<br />    True<br />tiber07vm4:<br />    True<br />{code}</p>
<p>h5. Sample run :</p>
<p>{code}<br />[root@tiber07vm2 ~]# salt-ssh  'tiber07vm4'  -r  'uptime'<br />tiber07vm4:<br />     02:38:11 up 20 days, 14:16,  1 user,  load average: 0.09, 0.08, 0.02</p>
<p>[root@tiber07vm2 ~]# salt-ssh  '*'  -r  'uptime'<br />tiber07vm2:<br />     02:38:22 up 20 days, 14:16,  1 user,  load average: 0.08, 0.08, 0.02<br />tiber07vm4:<br />     02:38:23 up 20 days, 14:16,  1 user,  load average: 0.08, 0.08, 0.02<br />{code}</p>
<p>h5. Known Errors and fixes:</p>
<p>{code}[root@tiber07vm2 ~]# salt-ssh  'tiber07vm2'  -r  'uptime'<br />OSError: [Errno 38] Function not implemented<br />{code}</p>
<p>Ohh LXC\!\!, You will get python OSError because of not to write /dev/shm (tmpfs), so to enable it&nbsp; update your /dev/shm mount options (rw, noexec) and remount /dev/shm.</p>
<p>{code}<br />[root@tiber07vm2 ~]# cat /etc/fstab<br />/dev/root               /                       rootfs   defaults        0 0<br />none                    /dev/shm                tmpfs    rw,nosuid,nodev,noexec    0 0<br />#none                    /dev/shm                tmpfs    nosuid,nodev    0 0</p>
<p>[root@tiber07vm2 ~]# mount /dev/shm<br />{code}</div>
