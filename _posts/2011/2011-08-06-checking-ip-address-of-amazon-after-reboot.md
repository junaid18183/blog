---
layout: post
title: checking Ip address of amazon after reboot
author: juned
categories: [Cloud,Bash]
tags: [Bash,Cloud]
image: assets/images/aws.jpg
featured: false
hidden: true
comments: true
---
# checking Ip address of amazon after reboot

Every time you reboot or stop/start an instance, you are assigned new public and private IP addresses and hostnames with this script you can get the new IP and hostname of instance, so that you can use it later

```
#!/bin/sh
META=http://169.254.169.254/latest/meta-data
HOSTNAME=$(/usr/bin/curl -s $META/hostname | /bin/sed 's+\..*++g')
hostname $HOSTNAME
echo $HOSTNAME > /etc/hostname
IPV4=$(/usr/bin/curl -s $META/public-ipv4)
echo "IPV4 $IPV4"
```

This http://169.254.169.254 is an internal Amazon EC2 server that will report  information about your instance. Very helpful if you haven’t installed  the EC2 API tools.
