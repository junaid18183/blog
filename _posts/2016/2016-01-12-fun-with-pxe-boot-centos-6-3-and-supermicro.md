---
layout: post
title: Fun with PXE boot Centos 6.3 and SuperMicro
author: juned
categories: [Linux,Networking]
tags: [Linux]
image: assets/images/linux.jpg
featured: true
hidden: false
comments: false
---
<p>Recently at <a href="http://www.corp.mode.com">work</a> we decided to upgrade our Hadoop capacity by adding new machines, the new machines bought were Supermicro <a href="http://www.supermicro.com/products/motherboard/Xeon/C600/X9DRL-7F.cfm">X9DRL-7F</a>.</p>
<p>I thought it would be pretty simple task to install OS on it as we already have the DHCP+TFTP setup followed by the Ansible role ( so piece of cake to install and provision machines ) and that too in production and in use for a while now.</p>
<p>&nbsp;</p>
<p>To my surprise the new machine were able to get the the DHCP lease ip but kickstart was not able to download, and that started a a funny troubleshooting journey.</p>
<p>To cut story short eventually it turns out that</p>
<blockquote><p>The  Supermicro -  <a href="http://www.supermicro.com/products/motherboard/Xeon/C600/X9DRL-7F.cfm">X9DRL-7F</a> is not compatible with Centos 6.3 , because the igb driver is pretty old in centos 6.3 kernel . ( surprisingly their OS compatibility <a href="http://www.supermicro.com/support/resources/OS/C602J.cfm">chart</a> doesn’t have this info )</p></blockquote>
<p>To fix the issue I have to</p>
<blockquote><p>Add the igb-4.3.0-1 support in the initial ramdisk of centos 6.3</p></blockquote>
<p>That fixed the PXE issue, except during PXE installation it flags the <strong>unsupported hardware detected</strong> warning  but the server was  provisioned using PXE.</p>
<p>But .. after the OS load and reboot the server didn't had the networking :(</p>
<p>I have fixed that only in ramdisk only actual kernel that's installed still had older version of igb ( 3.2.10-k ). So I decided to recompile the kernel with this new igb driver.</p>
<p>But .. then I realized that I can create a RPM out of  <a href="https://downloadcenter.intel.com/download/23093/Network-Adapter-Driver-for-82575-6-82580-I350-and-I210-211-Based-Gigabit-Network-Connections-for-Linux-">igb 4.3.0</a> source. I quickly created a RPM out of it tested on one of the centos 6.3 machine and added that RPM to our repo.</p>
<p>Finally I fixed thee kickstart of Centos 6.3 and added a section to install igb-4.3.0 rpm as a final step.</p>
<p>viola that worked like a charm</p>
<p>quite a work by the way.</p>
<p>&nbsp;</p>
<p>So if you are planning or have Supermicro X9DRL and facing issues with networking you know its igb driver that's playing naughty there.</p>
<p>&nbsp;</p>
<p>Edit :</p>
<p>I didn't faced the issue during our older hadoop deploy since the older hardware was different ( <a href="http://www.supermicro.com/products/motherboard/QPI/5500/X8DTL-6.cfm">SuperMicro X8DTL</a> ) so do the network driver.</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
