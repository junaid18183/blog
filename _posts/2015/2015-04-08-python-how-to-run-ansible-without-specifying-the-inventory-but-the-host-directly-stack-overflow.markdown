---
layout: post
title: python - How to run Ansible without specifying the inventory but the host directly?
  - Stack Overflow
date: 2015-04-08 13:25:38.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  _publicize_pending: '1'
---
<p>I know this question is really old but think that this little trick might helpful for future users who need help for this:ansible-playbook -i '10.254.3.133,' site.ymlif you run for local host:ansible-playbook -i 'localhost,' --connection=local site.ymlThe trick is that after ip address/dns name, put the comma inside the quotes.Hope this will help.</p>
<p>via <a href="http://stackoverflow.com/questions/17188147/how-to-run-ansible-without-specifying-the-inventory-but-the-host-directly">python - How to run Ansible without specifying the inventory but the host directly? - Stack Overflow</a>.</p>
