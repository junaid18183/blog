---
layout: post
title: PUPPET on Amazon EC2 (UBUNTU Machines)
date: 2012-07-11 07:53:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Puppet
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '7720950358865021933'
---
<div dir="ltr" style="text-align:left;">
<div></div>
<div align="center" class="MsoNormal"><b><span style="font-size:12pt;line-height:115%;">PUPPET on Amazon EC2 (UBUNTU Machines)</span></b></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><b><span style="font-size:12pt;line-height:115%;">Introduction:</span></b></div>
<div class="MsoNormal"><span style="font-size:12pt;line-height:115%;">Puppet is a system for automating system administration tasks. In the Puppet world, you define a policy (called a manifest) that describes the end state of your systems, and the Puppet software takes care of making sure the system meets that end state. If a file changes, it is replaced with a pristine copy. If a required package is removed, it is re-installed.</span></div>
<div class="MsoNormal"><span style="font-size:12pt;line-height:115%;">The Puppet system is split into two parts: a central server and the clients. The server runs a demon called puppetmaster. The clients run puppetd, which both connects to, and receives connections from, the puppetmaster. The manifest is written on the puppetmaster. If Puppet is used to manage the central server, it also runs the puppetd client.</span></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><img alt="" src="{{ site.baseurl }}/assets/hjSCKN3cX06PXfvgy+Xftx5GoWnzz3bXRaz9UuVMhbloCAIBIg5YAAMAg0BIAABgEWgIAAINASwAAYBBoCQAADAItAQCAQaAlAAAwCLQEAAAGgZYAAMAg0BIAABgEWgIAAINASwAAYBBoCQAADAItAQCAQaAlAAAwCLQEAAAGgZYAAMAg0BIAABgEWgIAAINASwAAYBBoCQAADAItAQCAQaAlAAAwCLQEAAAGgZYAAMAg0BIAABgEWgIAAINASwAAYBBoCQAADAItAQCAQaAlAAAwCLQEAAAGgZYAAMAg0BIAABgEWgIAAIP4b6isSxDKPiBaAAAAAElFTkSuQmCC" /><span style="font-size:12pt;line-height:115%;"> </span></div>
<div class="MsoNormal"><span style="font-size:12pt;line-height:115%;">                                                 </span><span style="font-size:12pt;line-height:115%;"></span></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><span style="font-size:12pt;line-height:115%;">                                                                                                                                       </span></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><span style="font-size:large;"><b><span style="line-height:115%;">Prerequisite:   Before we proceed we need to have few settings in place.</span></b></span></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"></div>
<ul style="text-align:left;">
<li><b><span style="line-height:115%;"></span></b><span>Enable ICMP on security group in which the client and server reside, so that ec2 instances can communicate/ reply to ping request. This is major requirement in troubleshooting while configuring. </span></li>
</ul>
<ul>
<li><b><span style="line-height:115%;"><span style="font-size-adjust:none;font-size:7pt;font-stretch:normal;font-style:normal;font-variant:normal;font-weight:normal;line-height:normal;"></span></span></b><span style="font-size:12pt;line-height:115%;">In order for the puppet server and the puppet client(s) to be able to communicate you should ensure that port 8140 is open between the systems.</span></li>
</ul>
<ul>
<li><b><span style="line-height:115%;"></span></b><b></b>D<span style="font-size:12pt;line-height:115%;">omain names- Prior to configuring puppet you may want to add a DNS record for puppet master and for puppet client So that can communicate with each other.</span></li>
</ul>
<div class="MsoListParagraphCxSpMiddle"></div>
<div class="MsoListParagraphCxSpMiddle"><span style="font-size:12pt;line-height:115%;"> In current minimal setup we are not using any DNS server. Instead we used /etc/hosts file to map hostname of client and server of Puppet</span></div>
<div class="MsoListParagraphCxSpMiddle"></div>
<div class="MsoListParagraphCxSpMiddle"><span style="font-size:12pt;line-height:115%;">Below is the snippet of /etc/hosts file on both client and server </span></div>
<div class="MsoListParagraphCxSpMiddle"></div>
<div class="MsoListParagraphCxSpMiddle"><i><span style="font-size:12pt;line-height:115%;">ubuntu@ip-10-205-2-127:~$ cat /etc/hosts</span></i></div>
<div class="MsoListParagraphCxSpMiddle"><i><span style="font-size:12pt;line-height:115%;">127.0.0.1 localhost</span></i></div>
<div class="MsoListParagraphCxSpMiddle"><i><span style="font-size:12pt;line-height:115%;">10.205.2.127 puppet.juned.com puppet</span></i></div>
<div class="MsoListParagraphCxSpMiddle"><i><span style="font-size:12pt;line-height:115%;">10.245.74.141 clinet.juned.com client</span></i></div>
<div class="MsoListParagraphCxSpMiddle"></div>
<div class="MsoListParagraphCxSpMiddle"><i><span style="font-size:12pt;line-height:115%;"># The following lines are desirable for IPv6 capable hosts</span></i></div>
<div class="MsoListParagraphCxSpMiddle"><i><span style="font-size:12pt;line-height:115%;">#::1 ip6-localhost ip6-loopback</span></i></div>
<div class="MsoListParagraphCxSpMiddle"><i><span style="font-size:12pt;line-height:115%;">#fe00::0 ip6-localnet</span></i></div>
<div class="MsoListParagraphCxSpMiddle"><i><span style="font-size:12pt;line-height:115%;">#ff00::0 ip6-mcastprefix</span></i></div>
<div class="MsoListParagraphCxSpMiddle"><i><span style="font-size:12pt;line-height:115%;">#ff02::1 ip6-allnodes</span></i></div>
<div class="MsoListParagraphCxSpMiddle"><i><span style="font-size:12pt;line-height:115%;">#ff02::2 ip6-allrouters</span></i></div>
<div class="MsoListParagraphCxSpLast"><i><span style="font-size:12pt;line-height:115%;">#ff02::3 ip6-allhosts</span></i></div>
<p><i><span style="font-size:12pt;line-height:115%;"><br style="page-break-before:always;" /></span></i> 
<div class="MsoNormal"></div>
<div class="MsoNormal"><b><span style="font-size:12pt;line-height:115%;">Puppet Server Installation and configuration:</span></b></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><b><span style="font-size:12pt;line-height:115%;">Install puppet master </span></b></div>
<div class="MsoNormal"><b><i><span style="font-size:12pt;line-height:115%;">a<span style="color:#eeeeee;">pt-get install puppetmaster</span></span></i></b></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><span style="font-size:12pt;line-height:115%;">Create Your Site Manifest file :</span></div>
<div class="MsoNormal"><span style="font-size:12pt;line-height:115%;">Puppet will start with /etc/puppet/manifests/site.pp as the primary manifest, so create /etc/puppet/manifests and add your manifest, along with any files it includes, to that directory. It is highly recommended that you use some form of version control (git, svn, etc) to keep track of changes to manifests.</span></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><span style="font-size:12pt;line-height:115%;">Example Manifest file, </span></div>
<div class="MsoNormal"><span style="font-size:12pt;line-height:115%;">package {</span></div>
<div class="MsoNormal"><span style="font-size:12pt;line-height:115%;">'apache2':</span></div>
<div class="MsoNormal"><span style="font-size:12pt;line-height:115%;">ensure =&gt; installed</span></div>
<div class="MsoNormal"><span style="font-size:12pt;">}</span></div>
<div class="MsoNormal"><span style="font-size:12pt;">service {</span></div>
<div class="MsoNormal"><span style="font-size:12pt;">'apache2':</span></div>
<div class="MsoNormal"><span style="font-size:12pt;">ensure =&gt; true,</span></div>
<div class="MsoNormal"><span style="font-size:12pt;">enable =&gt; true,</span></div>
<div class="MsoNormal"><span style="font-size:12pt;">require =&gt; Package['apache2']</span></div>
<div class="MsoNormal"><span style="font-size:12pt;line-height:115%;">}</span></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><span style="font-size:12pt;line-height:115%;">Next, create a node file /etc/puppet/manifests/nodes.pp with:</span></div>
<div class="MsoNormal"><span style="font-size:12pt;line-height:115%;">node '</span> <span style="font-size:12pt;line-height:115%;">clinet.juned.com ' {</span></div>
<div class="MsoNormal"><span style="font-size:12pt;line-height:115%;">include apache2</span></div>
<div class="MsoNormal"><span style="font-size:12pt;line-height:115%;">}</span></div>
<div class="MsoNormal"><span style="font-size:12pt;line-height:115%;">And now restart the puppet master </span></div>
<div class="MsoNormal"><b><span style="font-size:12pt;line-height:115%;">/etc/init.d/puppetmaster restart</span></b></div>
<div class="MsoNormal"><b><span style="font-size:12pt;line-height:115%;">Puppet Client (node) Installation and configuration:</span></b></div>
<div class="MsoNormal"><span style="font-size:12pt;line-height:115%;">apt-get install puppet</span></div>
<div class="MsoNormal"><span style="font-size:12pt;line-height:115%;">First, configure the puppet agent daemon to start. Edit /etc/default/puppet, changing START to</span></div>
<div class="MsoNormal"><span style="font-size:12pt;line-height:115%;">yes:</span></div>
<div class="MsoNormal"><span style="font-size:12pt;line-height:115%;">and now start the puppet client.</span></div>
<div class="MsoNormal"><b><span style="font-size:12pt;line-height:115%;">/etc/init.d/puppet start</span></b></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><span style="font-size:12pt;line-height:115%;">Now Edit file /etc/puppet/puppet.conf</span></div>
<div class="MsoNormal"><span style="font-size:12pt;line-height:115%;">Add line <b>server=</b><i> puppet.juned.com</i></span></div>
<p><b><span style="font-size:12pt;line-height:115%;"><br style="page-break-before:always;" /></span></b> 
<div class="MsoNormal"></div>
<div class="MsoNormal"><b><span style="font-size:12pt;line-height:115%;">Verifying Installation</span></b></div>
<div class="MsoNormal"><i><span style="font-size:12pt;line-height:115%;">Once Puppet is installed on that machine, run the agent against the central server to verify that everything is working appropriately. You should start the agent in verbose mode the first time and with the --waitforcert flag enabled:</span></i></div>
<div class="MsoNormal"><i><span style="font-size:12pt;line-height:115%;">Run this command from client node,</span></i></div>
<div class="MsoNormal"><i><span style="font-size:12pt;line-height:115%;"><span style="color:#eeeeee;">puppetd --server  puppet.juned.com</span> --waitforcert 60 --test</span></i></div>
<div class="MsoNormal"><span style="font-size:12pt;line-height:115%;"> On your server, list the waiting certificates </span></div>
<div class="MsoNormal"><span style="font-size:12pt;line-height:115%;">puppetca –list</span></div>
<div class="MsoNormal">You should see the name of the test agent node. Now go ahead and sign the certificate, <span style="font-size:12pt;line-height:115%;">then sign the certificate.</span></div>
<div class="MsoNormal"><span style="font-size:12pt;line-height:115%;">puppetca --sign  ip-10-245-74-141</span></div>
<div class="MsoNormal"><span style="font-size:12pt;line-height:115%;">That Request is accepted by puppet master and you can verify that on client end apche2 package is going to install you can also verify it by using <b>tail –f /var/log/syslog</b></span></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"></div>
<p><span><br style="page-break-before:always;" /></span> 
<div class="MsoNormal"></div>
<div class="MsoNormal"><span style="font-size:large;"><b>Pros and Cons of Puppet:</b></span></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><b>Pros:</b></div>
<div class="MsoListParagraphCxSpFirst">1.<span style="font-size-adjust:none;font-size:7pt;font-stretch:normal;font-style:normal;font-variant:normal;font-weight:normal;line-height:normal;">       </span>Automation of System Administration:<b> </b> </div>
<div class="MsoListParagraphCxSpMiddle">Puppet lets you perform normal administrative tasks (such as adding users, installing packages, and updating server configurations) by saving you countless hours of frustration, monotony, and/or reinventing the wheel on any number of systems, even if those systems are running completely different operating system.</div>
<div class="MsoListParagraphCxSpMiddle"></div>
<div class="MsoListParagraphCxSpMiddle">2.<span style="font-size-adjust:none;font-size:7pt;font-stretch:normal;font-style:normal;font-variant:normal;font-weight:normal;line-height:normal;">       </span>Security:</div>
<div class="MsoListParagraphCxSpMiddle">·<span style="font-size-adjust:none;font-size:7pt;font-stretch:normal;font-style:normal;font-variant:normal;font-weight:normal;line-height:normal;">         </span>Thorough security model (each client has its own SSL cert) Puppet comes with tools to make basic SSL setup and cert generation very painless (puppetca) </div>
<div class="MsoListParagraphCxSpMiddle">·<span style="font-size-adjust:none;font-size:7pt;font-stretch:normal;font-style:normal;font-variant:normal;font-weight:normal;line-height:normal;">         </span>Each client only gets to see the part of the site config that applies to it, not the whole site config</div>
<div class="MsoListParagraphCxSpLast">·<span style="font-size-adjust:none;font-size:7pt;font-stretch:normal;font-style:normal;font-variant:normal;font-weight:normal;line-height:normal;">         </span>Builtin file server where file access can be secured per-client (e.g. only hostX gets access to hostX/ssh_host_key)</div>
<div class="MsoNormal"></div>
<div class="MsoListParagraphCxSpFirst">3.<span style="font-size-adjust:none;font-size:7pt;font-stretch:normal;font-style:normal;font-variant:normal;font-weight:normal;line-height:normal;">       </span>Cross Platform:</div>
<div class="MsoListParagraphCxSpMiddle">works on most flavors of Unix/Linux (Fedora/RHEL/Debian/Gentoo, Solaris, OS X, some sort of *BSD)</div>
<div class="MsoListParagraphCxSpMiddle"></div>
<div class="MsoListParagraphCxSpMiddle">4.<span style="font-size-adjust:none;font-size:7pt;font-stretch:normal;font-style:normal;font-variant:normal;font-weight:normal;line-height:normal;">       </span>Domain-specific language for manifest :</div>
<div class="MsoListParagraphCxSpMiddle">·<span style="font-size-adjust:none;font-size:7pt;font-stretch:normal;font-style:normal;font-variant:normal;font-weight:normal;line-height:normal;">         </span>Clean abstraction from messy details of changing config </div>
<div class="MsoListParagraphCxSpMiddle">·<span style="font-size-adjust:none;font-size:7pt;font-stretch:normal;font-style:normal;font-variant:normal;font-weight:normal;line-height:normal;">         </span>Describe desired config of system, puppet figures out how to get there (e.g., you say 'need user X with homedir /foo and uid N', puppet figures out appropriate calls to useradd/usermod depending on whether user exists and fixes attributes that are out of sync) </div>
<div class="MsoListParagraphCxSpMiddle">·<span style="font-size-adjust:none;font-size:7pt;font-stretch:normal;font-style:normal;font-variant:normal;font-weight:normal;line-height:normal;">         </span>Abstraction: describe config in high-level terms (user, service, package, mount) for common config objects </div>
<div class="MsoListParagraphCxSpMiddle">·<span style="font-size-adjust:none;font-size:7pt;font-stretch:normal;font-style:normal;font-variant:normal;font-weight:normal;line-height:normal;">         </span>Templating support for things that can't/don't need to be described as objects; or distribute complete files</div>
<div class="MsoListParagraphCxSpMiddle">·<span style="font-size-adjust:none;font-size:7pt;font-stretch:normal;font-style:normal;font-variant:normal;font-weight:normal;line-height:normal;">         </span>Group config items logically with classes: can describe that a webserver has to have latest httpd package, service httpd enabled and running, and custom httpd.conf file from location X (that's not possible with at least one of the other config mgmt tools) </div>
<div class="MsoListParagraphCxSpLast">·<span style="font-size-adjust:none;font-size:7pt;font-stretch:normal;font-style:normal;font-variant:normal;font-weight:normal;line-height:normal;">         </span>Override mechanism for classes to allow for simple one-off (or hundred-off) tweaks, e.g. to take webserver class from above but use with different httpd.conf * Clean definition of what inputs can influence a client's config </div>
<div class="MsoNormal"></div>
<div class="MsoListParagraphCxSpFirst">5.<span style="font-size-adjust:none;font-size:7pt;font-stretch:normal;font-style:normal;font-variant:normal;font-weight:normal;line-height:normal;">       </span>Emphasis on practical usability, not research.</div>
<div class="MsoListParagraphCxSpMiddle">6.<span style="font-size-adjust:none;font-size:7pt;font-stretch:normal;font-style:normal;font-variant:normal;font-weight:normal;line-height:normal;">       </span>Cron-like support for scheduling tasks.</div>
<div class="MsoListParagraphCxSpMiddle">7.<span style="font-size-adjust:none;font-size:7pt;font-stretch:normal;font-style:normal;font-variant:normal;font-weight:normal;line-height:normal;">       </span>Tie-in with kickstart: provision basic system with ks (including puppet client), complete config with puppet.</div>
<div class="MsoListParagraphCxSpMiddle">8.<span style="font-size-adjust:none;font-size:7pt;font-stretch:normal;font-style:normal;font-variant:normal;font-weight:normal;line-height:normal;">       </span>Strong community support</div>
<div class="MsoListParagraphCxSpLast">9.<span style="font-size-adjust:none;font-size:7pt;font-stretch:normal;font-style:normal;font-variant:normal;font-weight:normal;line-height:normal;">       </span>Open source and free software</div>
<div class="MsoNoSpacing"></div>
<div class="MsoNormal"><b>Cons:</b></div>
<div class="MsoNoSpacing">1.<span style="font-size-adjust:none;font-size:7pt;font-stretch:normal;font-style:normal;font-variant:normal;font-weight:normal;line-height:normal;">       </span>All sysadmins are not programmer:</div>
<div class="MsoNoSpacing">                Ruby programming language is puppet's implementation language and we sysadmins are not familiar with Ruby.</div>
<div class="MsoNoSpacing"></div>
<div class="MsoNoSpacing">2.<span style="font-size-adjust:none;font-size:7pt;font-stretch:normal;font-style:normal;font-variant:normal;font-weight:normal;line-height:normal;">       </span>Puppet has its own language for configuration purpose and that one need to learn to configure puppet.               </div>
<div class="MsoNoSpacing">3.<span style="font-size-adjust:none;font-size:7pt;font-stretch:normal;font-style:normal;font-variant:normal;font-weight:normal;line-height:normal;">       </span>Puppet is a new software so not sure about count of servers and workstations efficiently managed by puppet.</div>
<div class="MsoNormal"></div>
<div class="MsoNormal"></div>
</div>
