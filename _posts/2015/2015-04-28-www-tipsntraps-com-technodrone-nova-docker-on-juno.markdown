---
layout: post
title: 'www.TipsNtrapS.com: Technodrone: Nova-Docker on Juno'
date: 2015-04-28 14:01:27.000000000 +05:30
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
<p>After enabling the docker as a hyper wiser support on my test one node open-stack implementation.</p>
<p>&nbsp;</p>
<p>I added another host in my nova compute farm, done slimier steps as in first (controller node)</p>
<p>but when I was booting up VM on that compute node It was giving error as "NoValidHost found".</p>
<p>On digging found that there was issues in neutron configuration. Dont know why packstack configured properly the neutron.conf.</p>
<p>&nbsp;</p>
<p>Have to copy the neutron.conf manually from controller to new nova compute host.</p>
<p>&nbsp;</p>
<p>New Error : Not Found (\"No such image: base-centos6\")</p>
<p>&nbsp;</p>
<p>Which turns out that the docker image base-centos6 was not present on the local nova box ( although present in glance ). So looks like while booting the docker vm its not able</p>
<p>to pull it from glance. ( will debug it later ) but for now. Have exported the image from controller as tar and imported on nova compute host.</p>
<p>&nbsp;</p>
<p>docker save image_name &gt; image_name.tar</p>
<p>scp image_name.tar newhost:/tmp</p>
<p>ssh newhost</p>
<p>docker load &lt; /tmp/image_name.tar</p>
<p>&nbsp;</p>
<p>Once again tried booting the VM on the new hosts , but this time the error was</p>
<p>&nbsp;</p>
<p>" Command: sudo nova-rootwrap /etc/nova/rootwrap.conf ln -sf /proc/11629/ns/net /var/run/netns/e59cc9600a720222ce7b746daa9", "code": 500, "details": "  File \"/usr/lib/python2.7/site-packages/nova/compute/manager.py\", line 2033, in _do_build_and_run_instance"</p>
<p>it turns out that the /etc/nova/rootwrap.d/docker.filters was not present on the new host. Once again copied that from controller to new hosts.</p>
<p>&nbsp;</p>
<p>This time the nova boot was successfull.</p>
<p>&nbsp;</p>
<p>So, although Nova - Docker works , you need to hack couple of things to get it working.</p>
<p>&nbsp;</p>
<p>Happy Hacking</p>
<p>&nbsp;</p>
