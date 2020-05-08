---
layout: post
title: Safely pairing HA-Proxy with virtual network interface providers like Keepalived
  or Heartbeat
date: 2014-12-30 14:27:36.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  _publicize_pending: '1'
  is_reblog: '1'
  post_id: '46'
  blog_id: '13441406'
  reblog_snapshot: "O:8:\"stdClass\":7:{s:5:\"title\";s:93:\"Safely pairing HA-Proxy
    with virtual network interface providers like Keepalived or Heartbeat\";s:4:\"type\";s:4:\"post\";s:9:\"mime_type\";s:0:\"\";s:6:\"format\";b:0;s:12:\"modified_gmt\";s:19:\"2011-12-07
    13:52:06\";s:9:\"permalink\";s:132:\"http://nbevans.wordpress.com/2011/03/01/safely-pairing-haproxy-with-virtual-network-interface-providers-like-keepalived-or-heartbeat\";s:7:\"content\";s:3817:\"<div
    class=\"reblogged-content\">\n\nThis is sort of a follow-up to the <a href=\"http://nbevans.wordpress.com/2011/02/27/deploying-ha-proxy-keepalived-with-mercurial-for-distributed-config/\">Deploying
    HA-Proxy + Keepalived with Mercurial for distributed config</a> post.\r\n\r\nDuring
    testing we were coming across an issue where the HA-Proxy instance running on
    the slave member of our cluster would fail to bind some of its frontend proxies:\r\n\r\n[sourcecode
    wraplines=\"false\" gutter=\"false\"]\r\nStarting haproxy: [ALERT] : Starting
    proxy Public-HTTPS: cannot bind socket\r\n[/sourcecode]\r\n\r\nAfter some head
    scratching I noticed that the problem was only arising on those proxies that explicitly
    defined the IP address of a virtual interface that was being managed by Keepalived
    (or maybe Heartbeat for you).\r\n\r\nThis is because both of these High-Availability
    clustering systems use a rather simplistic design whereby the \"shared\" virtual
    IP is only installed on the <em>active</em> node in the cluster. While the nodes
    that are in a dormant state (i.e. the slaves) do not actually have those virtual
    IPs assigned to them during that state. It's a sort of \"IP address hot-swapping\"
    design. I learnt this by executing a simple a command, first from the master server:\r\n\r\n[sourcecode
    wraplines=\"false\" gutter=\"false\" highlight=\"6,7\"]\r\n$ ip a\r\n&lt;snipped
    stuff for brevity&gt;\r\n2: seth0:  mtu 1500 qdisc pfifo_fast qlen 1000\r\n    link/ether
    00:15:5d:28:7d:19 brd ff:ff:ff:ff:ff:ff\r\n    inet 172.16.61.151/24 brd 172.16.61.255
    scope global seth0\r\n    inet 172.16.61.150/24 brd 172.16.61.255 scope global
    secondary seth0:0\r\n    inet 172.16.61.159/24 brd 172.16.61.255 scope global
    secondary seth0:1\r\n    inet6 fe80::215:5dff:fe28:7d19/64 scope link\r\n       valid_lft
    forever preferred_lft forever\r\n&lt;snipped trailing stuff for brevity&gt;\r\n[/sourcecode]\r\n\r\nThen
    again, from the slave server:\r\n\r\n[sourcecode wraplines=\"false\" gutter=\"false\"]\r\n$
    ip a\r\n&lt;snipped stuff for brevity&gt;\r\n2: seth0:  mtu 1500 qdisc pfifo_fast
    qlen 1000\r\n    link/ether 00:15:5d:2d:9c:11 brd ff:ff:ff:ff:ff:ff\r\n    inet
    172.16.61.152/24 brd 172.16.61.255 scope global seth0\r\n    inet6 fe80::215:5dff:fe2d:9c11/64
    scope link\r\n       valid_lft forever preferred_lft forever\r\n&lt;snipped trailing
    stuff for brevity&gt;\r\n[/sourcecode]\r\n\r\nUnfortunately this behaviour can
    cause problems for programs like HA-Proxy which have been configured to expect
    the existence of specific network interfaces on the server. I was considering
    working around it by writing some scripts that hook events within the HA cluster
    to handle stopping and starting the HA-Proxy when needed. But this approach seemed
    clunky and unintuitive. So I dug a little deeper and came across a bit of a gem
    hidden away in the depths of the Linux networking stack. It is a simple boolean
    setting called \"<code>net.ipv4.ip_nonlocal_bind</code>\" and it allows a program
    like HA-Proxy to create listening sockets on network interfaces that do not actually
    exist on the server. It was created specially for this situation.\r\n\r\nSo in
    the end the fix was as simple as adding/updating the <code>/etc/sysctl.conf</code>
    file to include the following key/value pair:\r\n\r\n[sourcecode wraplines=\"false\"
    gutter=\"false\"]\r\nnet.ipv4.ip_nonlocal_bind=1\r\n[/sourcecode]\r\n\r\nMy previous
    experience of setting up these low-level High-Availability clusters was with Windows
    Server's feature called Network Load Balancing (NLB). This works quite different
    from Keepalived and Heartbeat. It relies upon some low level ARP hacking/trickery
    and some sort of distributed time splicing algorithm. But it does ensure that
    each node in the cluster (whether in a master or slave position) will remain allocated
    with the virtual IP address(es) at all times. I suppose there is always more than
    one way to crack an egg...</div>\";}"
---

