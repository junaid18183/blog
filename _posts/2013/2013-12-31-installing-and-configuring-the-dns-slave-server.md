---
layout: post
title: Installing and Configuring the DNS slave Server.
description: Installing and Configuring the DNS slave Server.
author: juned
categories: [Linux,DNS]
tags:  [Linux,DNS]
image: assets/images/linux.jpg
featured: true
hidden: false
comments: false
---
# Installing and Configuring the DNS slave Server.

We are using the chrooted environment for Bind. so that the base configuration path would be `/var/named/chroot/var/named`

For non glam dns we will build the caching name server.
### Install the required packages
```
# yum update -y# yum install bind bind-utils -y
# yum install bind-chroot -y
#yum install caching-nameserver.x86_64
```
You should have following packages installed,
```
bind-chroot-9.3.6-20.P1.el5_8.5bind-9.3.6-20.P1.el5_8.5ypbind-1.19-12.el5_6.1bind-utils-9.3.6-20.P1.el5_8.5bind-libs-9.3.6-20.P1.el5_8.5caching-nameserver-9.3.6-20.P1.el5_8.5
```
### Next step would be to create the named.conf file. 
Rather than  creating it from scratch, it would be much easier to copy it from any existing slave server.
So take backup of existing `/etc/named.conf` and scp the  `named.conf` file from existing slave server at location 
`/var/named/chroot/etc/named.conf`
And then create the softlink
`# ls -l /etc/named.conflrwxrwxrwx 1 root root 32 Oct 17 00:50 /etc/named.conf -&gt; /var/named/chroot/etc/named.conf`

Verify the named configuration, using below command

`named-checkconf ; echo $?0`

### Master server setup
On master you have to perform two major changes,
* Edit the named.conf and add the IP range of the new slave server in the acl "my_networks"
* Add the NS record of new slave server in every zone file, e.g.
```
;  This is a list of all of the named servers for this domain.   The first;  is the primary (us) and the rest are our various secondaries;;  WARNING: cannot list as a nameserver any machine that forwards to mac
@                       IN      NS              tiber.tipsntraps.com@                       IN      NS              slavetiber.tipsntraps.com
```
* Restart the named on both master and slave.
make sure you perform the configtest before restarting the named.
### how to perform the confitest
```
# named-checkconf ; echo $?0
# /etc/init.d/named configtestzone tipsntraps.com/IN: loaded serial 2013121908
```

### Make sure all the zone files are transferred in the newly configured slave properly, the zone defination files would be located at,
`/var/named/chroot/var/named/slaves/`
### Testing
Change the Serial of one of the zone file on master and do rndc reload , confirm that the change is propagated successfully on the new slave.
### Monitoring
We have DNS-Zone-CHECK monitoring in place on master server, which checks that all the zone files defined in master are also setup on the slave server. This monitoring also checks the Serial of every domain of slave server against the master server.
To enable this monitoring, add  the line in file ```
`/etc/check_mk/mrpe.cfg`
Note- please pass the appropriate slave server name as second argument
### DNS zone check for rsukapp2DNS-ZONE-CHECK-slavename /etc/nagios/scripts/check_dns_slave.sh    
```
once you have added this line in mrpe.cfg, take the re-inventory of the master dns server in check_mk and restart it.
```
