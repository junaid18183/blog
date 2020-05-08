---
layout: post
title: Network Infrastructure monitoring tools
date: 2012-06-26 13:25:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '942857341503139810'
---
<div dir="ltr" style="text-align:left;">
<div class="separator" style="clear:both;text-align:center;"><a href="http://junaid18183.files.wordpress.com/2012/06/43499-mon-tools.png" style="margin-left:1em;margin-right:1em;"><img border="0" height="92" src="{{ site.baseurl }}/assets/43499-mon-tools.png?w=300" width="320" /></a></div>
<p><b>What is Cacti?</b></p>
<p>Cacti is a complete front-end to RRDTool  ((Round Robin Database tool is a system to store and display time-series  data.), it stores all of the necessary information to create graphs and  populate them with data in a <span class="IL_AD" id="IL_AD1">MySQL database<span class="IL_AD_ICON"></span></span>.<br />The front-end is completely PHP driven. <br />Along with being able to maintain Graphs, <span class="IL_AD" id="IL_AD2">Data Sources<span class="IL_AD_ICON"></span></span>,  and Round Robin Archives in a database, cacti handle’s the data  gathering. There is also SNMP support for those used to creating traffic  graphs with MRTG.</p>
<p><b>Data Sources</b><br />To handle data gathering, you can feed cacti the paths to any external script/command along with any data that <span class="IL_AD" id="IL_AD6">the user<span class="IL_AD_ICON"></span></span> will need to "fill in", cacti will then gather this data in a cron-job and populate a MySQL database/the round robin archives.</p>
<p>Data Sources  can also be created, which correspond to actual data on the graph. For  instance, if a user would want to graph the ping times to a host, you  could create a <span class="IL_AD" id="IL_AD3">data source<span class="IL_AD_ICON"></span></span> utilizing a script that pings a host and returns it's value in  milliseconds. After defining options for RRDTool such as how to store  the data you will be able to define any <span class="IL_AD" id="IL_AD4">additional information<span class="IL_AD_ICON"></span></span> that the data input source requires, such as a host to ping in this case. Once a data source is created, it is automatically maintained at 5 minute intervals.</p>
<p><b>Graphs</b><br />Once one or more data sources  are defined, an RRDTool graph can be created using the data. Cacti  allows you to create almost any imaginable RRDTool graph using all of  the standard RRDTool graph types and consolidation functions. A color <span class="IL_AD" id="IL_AD11">selection<span class="IL_AD_ICON"></span></span> area and automatic text padding function also aid in the creation of graphs to make the process easier.</p>
<p>Not  only can you create RRDTool based graphs in cacti, but there are many  ways to display them. Along with a standard "list view" and a "preview  mode", which resembles the RRDTool frontend 14all, there is a "tree  view", which allows you to put graphs onto a <span class="IL_AD" id="IL_AD7">hierarchical<span class="IL_AD_ICON"></span></span> tree for organizational purposes.</p>
<p><b>User Management</b><br />Due  to the many functions of cacti, a user based management tool is built  in so you can add users and give them rights to certain areas of cacti.  This would allow someone to create some users that can change graph  parameters, while others can only view graphs. Each user also maintains  their own settings when it comes to viewing graphs.</p>
<p><b>Templating</b><br />Lastly, cacti is able to scale to a large number of data sources and graphs through the use of templates. This allows the creation of a single graph or data source template which defines any graph or data source  associated with it. Host templates enable you to define the  capabilities of a host so cacti can poll it for information upon the  addition of a new host.</p>
<p><b>Support</b></p>
<p>Linux, Windows </p>
<p><b>Licensing/Donations</b></p>
<p>Cacti is released under the GNU General Public License, <span class="IL_AD" id="IL_AD5">meaning<span class="IL_AD_ICON"></span></span> that it is completely free with no strings attached. However, if you  enjoy Cacti and find it useful be sure to check out my donations page  for various ways to encourage development and otherwise make me happy.</p>
<p><b><span class="IL_AD" id="IL_AD12">Website<span class="IL_AD_ICON"></span></span></b></p>
<p><a href="http://cacti.net/">http://cacti.net</a></p>
<p><b>Opennms</b></p>
<p>OpenNMS is the world's first enterprise <span class="IL_AD" id="IL_AD4">grade<span class="IL_AD_ICON"></span></span> network management <span class="IL_AD" id="IL_AD3">platform<span class="IL_AD_ICON"></span></span> developed under the open source model. It consists of a community  supported open-source project as well as a commercial services,  training, and support organization.</p>
<p><b>Website </b><br />http://www.opennms.com/site/</p>
<p><b>Licence</b></p>
<p>GPL</p>
<p><b>Munin</b></p>
<p>Munin the <span class="IL_AD" id="IL_AD1">monitoring tool<span class="IL_AD_ICON"></span></span> surveys all your computers and remembers what it saw. It <span class="IL_AD" id="IL_AD3">presents<span class="IL_AD_ICON"></span></span> all the information in graphs through a web interface. Its emphasis is  on plug and play capabilities. After completing a installation a high  number of monitoring plugins will be playing with no more effort. </p>
<p>Using Munin you can easily monitor the performance of your computers, networks, SANs, <span class="IL_AD" id="IL_AD2">applications<span class="IL_AD_ICON"></span></span>,  weather measurements and whatever comes to mind. It makes it easy to  determine "what's different today" when a performance problem crops up.  It makes it easy to see how you're doing capacity-wise on any resources.  <br />Support:- Linux/Windows </p>
<p><b>Website</b></p>
<p>http://munin.projects.linpro.no</p>
<p><b>Big Sister</b></p>
<p>The Big Sister network monitor is a real time system and network health monitoring application.</p>
<p><b>Functions </b><br />•   monitor networked systems <br />•   provide a simple real-time view of the current network status <br />•   notify you when your systems are becoming critical <br />•   generate a history of status changes <br />•   log and display a variety of system performance data </p>
<p><b>Licence</b></p>
<p>GNU General Public License</p>
<p><b>Website</b></p>
<p>http://www.bigsister.ch/snapshots.html</p>
<p><b>Zenoss</b><br />Zenoss provides a complete suite of software and services to help you succeed monitoring your IT <span class="IL_AD" id="IL_AD3">infrastructure<span class="IL_AD_ICON"></span></span>.</p>
<p>Screenshots:- http://www.zenoss.com/product/screenshots</p>
<p><b>Licence</b><br />GPL</p>
<p><b>Support</b><br />Linux</p>
<p><b>Website </b><br />http://www.zenoss.com/product/</p>
<p><a name="more"></a><b>Big brother </b></p>
<p>Big Brother is a combination of monitoring  methods. Unlike SNMP where information is just collected and devices  polled, Big Brother is designed in such a way that each local system  broadcasts its own information to a central location. Simultaneously,  Big Brother also polls all networked systems from a central location.  This creates a highly efficient and redundant method for proactive  network monitoring.</p>
<p><b>Features</b></p>
<p>Display</p>
<p>Big  Brother displays status information as web pages or WML pages for  WAP-enabled devices. These web pages have the systems monitored down the  left hand side of the page, the tests for each system across the top of  the page. This <span class="IL_AD" id="IL_AD4">results in<span class="IL_AD_ICON"></span></span> a matrix of color coded dots on screen. Green is Good, Red is Bad. In addition, the background color of <span class="IL_AD" id="IL_AD11">the status<span class="IL_AD_ICON"></span></span> pages is always the color of the most serious condition of any element being monitored at that time. <br />Architecture</p>
<p>Big  Brother uses a client-server architecture combined with methods which  both push and pull data. Network testing is done by polling all  monitored services from a single machine, and reporting these results to  a central location (the BBDISPLAY). If you want local <span class="IL_AD" id="IL_AD10">system information<span class="IL_AD_ICON"></span></span>,  you can install a BB client on the local machine, which will send CPU,  process, disk space, and logfile status reports in periodically. Each  report is timestamped with an expiration date (like milk). This lets us  know when a report is no longer valid, which is usually an indication of  a more serious problem. <br />Redundancy</p>
<p>It's not much good if your <span class="IL_AD" id="IL_AD8">monitoring system<span class="IL_AD_ICON"></span></span> can fail and not tell you of the problem. Big Brother supports  redundancy through allowing you to run multiple instances of Big Brother  in parallel. This means that BB clients can report into multiple Web  Displays (BBDISPLAYs) and <span class="IL_AD" id="IL_AD2">Notification<span class="IL_AD_ICON"></span></span> servers (BBPAGERs). <br />Protocol</p>
<p>Big  Brother sends all status reports from client to server over port 1984.  What other port would Big Brother use? The IANA has assigned Big Brother  this port, and the BB protocol itself is open. Limited support for SNMP  trap handling is supported using third-party plugins. <br />Platforms</p>
<p>The  Big Brother servers and BBNET functions run on Unix/Linux, with a  scaled-down version for NT/Win2K is also available. Client software is  available for Unix/Linux, NT/Win2K/Win2003 while user contributed  clients for Netware, Mac OS 9, VMS, AS/400 and VM/ESA at  http://www.deadcat.net. <br />Network tests</p>
<p>Big Brother includes  support for testing ftp, http, https, smtp, pop3, dns, telnet, imap,  nntp, and ssh servers. Support for additional tests is easily added. <br />Local Tests</p>
<p>If  you choose to install a BB client on a local machine, it will monitor  disk space, CPU usage, messages, and can check that important processes  are up and running. <br />Notification</p>
<p>Big Brother has a  sophisticated notification ruleset, not for the faint of heart (blame  Rob). You can notify based on time-of-day, machine, or the test that  failed. In addition we support an initial delay before paging (useful to  cut down on late night false alarms), page-only-every defined amount of  time, paging groups, <span class="IL_AD" id="IL_AD7">acknowledgement<span class="IL_AD_ICON"></span></span>,  and escalation. Built in support for e-mail paging, alphanumeric paging  via Qpage or Sendpage, or numeric and SMS pages via Kermit for the BB  Unix/<span class="IL_AD" id="IL_AD12">Linux server<span class="IL_AD_ICON"></span></span> platform while the NT/Win2K server platform only supports e-mail for now. Under the Unix/Linux server platform, you can even create your own custom notification procedure. <br />History &amp; Reporting</p>
<p>Big  Brother supports reporting, which will allow you to determine whether  Service Level Agreements are being met. In addition, we provide access  to historical status information so you can see what the problem was at  any given time. <br />Plug-ins &amp; Extensions</p>
<p>Big Brother  supports plug-ins. You can write plug-ins in any language, and we  include several samples to make it easy. In addition, Brothers from  around the world have written hundreds of plug-ins to monitor everything  from <span class="IL_AD" id="IL_AD9">Oracle Databases<span class="IL_AD_ICON"></span></span> to CPU temperature on Solaris machines. You can see the current list at http://www.deadcat.net. <br />Flexibility</p>
<p>Big  Brother is very flexible. Warning and alarm levels are all easily  redefinable. The Web Display can be easily customized. We have hooks  into other products, like MRTG for <span class="IL_AD" id="IL_AD5">bandwidth monitoring<span class="IL_AD_ICON"></span></span>. Since you have the <span class="IL_AD" id="IL_AD6">source code<span class="IL_AD_ICON"></span></span>, you can easily figure out what Big Brother is doing, and change it to suit your needs. <br />Community</p>
<p>One  of the best things about Big Brother is the community that has sprung  up around it. Over 2000 Brothers on the various mailing list provide  quick and friendly support and commentary. </p>
<p><b>Licence</b><br />Big  Brother is distributed under our Better than Free license. Clause 2  from that license determines whether you need to buy a Commercial  license.</p>
<p><b>Website </b></p>
<p>http://www.bb4.org </p></div>
