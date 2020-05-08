---
layout: post
title: How to execute task on subset of hosts - Ansible
date: 2015-01-07 14:31:12.000000000 +05:30
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
  _wpas_skip_facebook: '1'
  _wpas_skip_google_plus: '1'
  _wpas_skip_twitter: '1'
  _wpas_skip_linkedin: '1'
  _wpas_skip_tumblr: '1'
  _wpas_skip_path: '1'
---
<p>Host file</p>
<p>[root@tiber ~]# cat hosts.yml<br />
[nodes]<br />
tiber<br />
po<br />
docker</p>
<p>I want to run task on 2ND &amp; 3RD HOSTS only.</p>
<p>[root@tiber ~]# cat play.yml<br />
- hosts: all<br />
tasks:<br />
- shell: "hostname"<br />
when: inventory_hostname != play_hosts[0]<br />
[root@tiber ~]# ansible-playbook -i hosts.yml play.yml<br />
[WARNING]: The version of gmp you have installed has a known issue regarding<br />
timing vulnerabilities when used with pycrypto. If possible, you should update<br />
it (ie. yum update gmp).</p>
<p>PLAY [all] ********************************************************************</p>
<p>GATHERING FACTS ***************************************************************<br />
ok: [docker]<br />
ok: [tiber]<br />
ok: [po]</p>
<p>TASK: [shell hostname] ********************************************************<br />
skipping: [tiber]<br />
changed: [docker]<br />
changed: [po]</p>
<p>PLAY RECAP ********************************************************************<br />
docker : ok=2 changed=1 unreachable=0 failed=0<br />
po : ok=2 changed=1 unreachable=0 failed=0<br />
tiber : ok=1 changed=0 unreachable=0 failed=0</p>
