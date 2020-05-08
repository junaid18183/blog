---
layout: post
title: Adding docker as virtualzation driver in Openstack
date: 2015-03-27 10:07:56.000000000 +05:30
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
<pre class="prettyprint"><code><span class="com"># yum install python-pbr python-pip</span>
<span class="com"># yum install docker-io -y</span>
<span class="com"># git clone https://github.com/stackforge/nova-docker</span>
<span class="com"># cd nova-docker</span>
<span class="com"># git checkout stable/juno</span>
<span class="com"># python setup.py install</span>
<span class="com"># systemctl start docker</span>
<span class="com"># systemctl enable docker

Now enable docker in nova and glance 
</span></code></pre>
<div class="line number5 index4 alt2"><code class="java plain">cp /etc/nova/nova.conf /etc/nova/nova.conf.orig</code></div>
<div class="line number6 index5 alt1"><code class="java plain">diff /etc/nova/nova.conf /etc/nova/nova.conf.orig</code></div>
<div class="line number7 index6 alt2"><code class="java value">2006</code><code class="java plain">,2009c2006</code></div>
<div class="line number8 index7 alt1"><code class="java plain">&lt; #compute_driver=nova.virt.libvirt.LibvirtDriver</code></div>
<div class="line number9 index8 alt2"><code class="java plain">&lt;</code></div>
<div class="line number10 index9 alt1"><code class="java plain">&lt; #Changed by Juned</code></div>
<div class="line number11 index10 alt2"><code class="java plain">&lt; compute_driver = novadocker.virt.docker.DockerDriver</code></div>
<div class="line number12 index11 alt1"><code class="java plain">---</code></div>
<div class="line number13 index12 alt2"><code class="java plain">&gt; compute_driver=nova.virt.libvirt.LibvirtDriver</code></div>
<div class="line number14 index13 alt1"><code class="java plain">cp /etc/glance/glance-api.conf /etc/glance/glance-api.conf.orig</code></div>
<div class="line number15 index14 alt2"><code class="java plain">[root</code><code class="java color1">@ggvaapp08</code> <code class="java plain">nova-docker(keystone_admin)]# diff /etc/glance/glance-api.conf /etc/glance/glance-api.conf.orig</code></div>
<div class="line number16 index15 alt1"><code class="java value">108</code><code class="java plain">,110d107</code></div>
<div class="line number17 index16 alt2"><code class="java plain">&lt; #Added By JunedM</code></div>
<div class="line number18 index17 alt1"><code class="java plain">&lt; container_formats=ami,ari,aki,bare,ovf,ova,docker</code></div>
<div class="line number19 index18 alt2"></div>
<div class="line number19 index18 alt2"></div>
<div class="line number19 index18 alt2">Also make sure the docker api version for server and client are same otherwise nova will not start.</div>
<div class="line number19 index18 alt2"></div>
<div class="line number19 index18 alt2">[root@tiber ~]# docker version<br />
Client version: 1.3.2<br />
Client API version: 1.15<br />
Go version (client): go1.3.3<br />
Git commit (client): 39fa2fa/1.3.2<br />
OS/Arch (client): linux/amd64<br />
Server version: 1.3.2<br />
Server API version: 1.15<br />
Go version (server): go1.3.3<br />
Git commit (server): 39fa2fa/1.3.2</div>
<div class="line number19 index18 alt2"></div>
<div class="line number19 index18 alt2">Docker Client is docker-py</div>
<div class="line number19 index18 alt2"></div>
<div class="line number19 index18 alt2">[root@tiber~]# pip list | grep docker<br />
docker-py (1.0.0)<br />
nova-docker (0.0.0.post140)</div>
<div class="line number19 index18 alt2"></div>
<div class="line number19 index18 alt2">&gt;&gt;&gt; from docker import Client<br />
&gt;&gt;&gt; c = Client(base_url='unix://var/run/docker.sock')<br />
&gt;&gt;&gt; c.containers()<br />
Traceback (most recent call last):<br />
File "&lt;stdin&gt;", line 1, in &lt;module&gt;<br />
File "/usr/lib/python2.7/site-packages/docker/client.py", line 423, in containers<br />
res = self._result(self._get(u, params=params), True)<br />
File "/usr/lib/python2.7/site-packages/docker/client.py", line 123, in _result<br />
self._raise_for_status(response)<br />
File "/usr/lib/python2.7/site-packages/docker/client.py", line 119, in _raise_for_status<br />
raise errors.APIError(e, response, explanation=explanation)<br />
docker.errors.APIError: 404 Client Error: Not Found ("client and server don't have same version (client : 1.17, server: 1.15)")<br />
&gt;&gt;&gt; exit<br />
Use exit() or Ctrl-D (i.e. EOF) to exit<br />
&gt;&gt;&gt;</div>
<pre class="prettyprint"><code><span class="com"> </span></code></pre>
