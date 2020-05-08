---
layout: post
title: DNS replication slow
description: DNS replication slow
author: juned
categories: [Linux,DNS]
tags:  [Linux,DNS]
image: assets/images/linux.jpg
featured: true
hidden: false
comments: false
---
# DNS replication slow
Recently at [work](http://www.ning.com/) I added two new DNS slave servers. 
We are using BIND 9 as a DNS server.
To my surprise I noticed that the the slave replication on these two boxes were extremely slow, infact after changing the SOA of the zone file it  was taking almost hours to replicate that to these slave boxes.

The other slave boxes were working perfectly fine.
I started digging into it.
`/etc/named.conf` on both the slaves was looking fine , in fact it was copied from the older running slave servers.
From master the telnet to port 53 was working.
There was no symptoms of any error in the log files.

# The gotcha :
after much of debugging and goggling I found the gotcha, that none of the zone files on my master had declared these new slave servers as NS. so ... I added those entries chnaged the serial and restarted named on master. And issue resolved.
```
@                       IN      NS              tiber1.tipsntraps.com.
@                       IN      NS              tiber1.tipsntraps.com.
```

### Conclusion :
After looking around I found that -
When the serial number is changed on the master, it will notify the slave immediately. 
In other words,notify is enabled by default. 
BUT, the way notify works is, the master looks at the NS records of that particular domain in the zone file, and notifies the servers listed in the NS record, excluding itself.
If your slave server's hostname is not  listed as an NS record in the zone file;  The slave will  contact the master, listed in the slave's config file - masters { X.X.X.X; }; at the defined Refresh interval. 
And that is why it is taking long time to update to the slave initially.
