---
layout: post
title: Nagios-Installation
date: 2012-06-26 13:39:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '6374948800528741219'
---
<div dir="ltr" style="text-align:left;">Nagios is an open source host, service and network monitoring program.  It is designed to run under Linux, although it should work under most  other *NIX variants. It can run either as a normal process or as a  daemon, intermittently running checks on various services that you  specify. The actual service checks are performed by external "<span class="IL_AD" id="IL_AD8">plug-in<span class="IL_AD_ICON"></span></span>"  which return service information to Nagios. Several CGI programs are  included with Nagios in order to allow you to view the current service  status, history, etc. via a web browser.</p>
<p>Nagios has a lot of features, making it a very powerful <span class="IL_AD" id="IL_AD3">monitoring tool<span class="IL_AD_ICON"></span></span>. Some of the major features are listed below: <br />•   Monitoring of <span class="IL_AD" id="IL_AD2">network services<span class="IL_AD_ICON"></span></span> (SMTP, POP3, HTTP, NNTP, PING, etc.) <br />•   Monitoring of host resources (processor load, disk and memory usage, running processes, <span class="IL_AD" id="IL_AD5">log files<span class="IL_AD_ICON"></span></span>, etc.) <br />•   Monitoring of environmental factors such as temperature <br />•   Simple plugin design that allows users to easily develop their own host and service checks <br />•   Ability  to define network host hierarchy, allowing detection of and distinction  between hosts that are down and those that are unreachable <br />•   Contact notifications when service or host problems occur and get resolved (via email, pager, or other user-defined method) <br />•   Optional escalation of host and service notifications to different contact groups <br />•   Ability to define event handlers to be run during service or host events for proactive problem resolution <br />•   Support for implementing redundant and distributed monitoring servers <br />•   External command interface that allows on-the-fly modifications to be made to the monitoring and <span class="IL_AD" id="IL_AD4">notification<span class="IL_AD_ICON"></span></span> behavior through the use of event handlers, the web interface, and third-party <span class="IL_AD" id="IL_AD7">applications<span class="IL_AD_ICON"></span></span> <br />•   Retention of host and service status across program restarts <br />•   Scheduled downtime for suppressing host and service notifications during periods of planned outages <br />•   Ability to acknowledge problems via the web interface <br />•   Web interface for viewing current network status, notification and problem history, log file, etc. <br />•   Simple authorization scheme that allows you restrict what users can see and do from the web interface </p>
<p><b>License </b></p>
<p>Nagios  is licensed under the terms of the GNU General Public License Version 2  as published by the Free Software Foundation. This gives you legal  permission to copy, distribute and/or modify Nagios under certain  conditions. Read the 'LICENSE' file in the Nagios distribution or read  the online version of the license for <span class="IL_AD" id="IL_AD1">more details<span class="IL_AD_ICON"></span></span>.  Nagios is provided AS IS with NO WARRANTY OF ANY KIND, INCLUDING THE  WARRANTY OF DESIGN, MERCHANTABILITY, AND FITNESS FOR A PARTICULAR  PURPOSE. </p>
<p><b>Support</b></p>
<p>Linux </p>
<p><b>Website </b></p>
<p>http://www.nagios.org/about/screenshots.php</p>
<p> <span style="text-decoration:underline;">Installing Nagios</span></p>
<p><b>* Important: </b>Installing  and configuring Nagios is rather involved. You can't just compile the  binaries, run the program and sit back. There's a lot to setup before  you can actually start monitoring anything. Relax, take your time and  read all the documentation - you're going to need it. Okay, let's get  started...</p>
<p><b>Become Root:</b> </p>
<p>You'll need to have root  access to install Nagios as described in this documentation, as you'll  be creating users and group, modifying your web server config files,  etc. Either login as root before you begin or use the su command to  change to the root user from another account.</p>
<p><b>Getting The Latest Version</b></p>
<p>You can download the latest version of Nagios from <span style="text-decoration:underline;"><i>http://www.nagios.org/</i></span> download.</p>
<p><b>Unpacking The Distribution</b></p>
<p>To unpack the Nagios distribution, use the following command:</p>
<p><b>#tar xzf nagios-version.tar.gz</b></p>
<p>When  you have finished executing these commands, you should find a  nagios-version directory that has been created in your current  directory. Inside that directory you will find all the files that  comprise the core Nagios distribution.</p>
<p><b>Create Nagios User/Group</b></p>
<p>You're probably going to want to run Nagios under a normal <span class="IL_AD" id="IL_AD9">user account<span class="IL_AD_ICON"></span></span>, so add a new user (and group) to your system with the following command (this will vary depending on what OS you're running):</p>
<p><b>#adduser nagios</p>
<p>Create Installation Directory</b></p>
<p>Create the base directory where you would like to install Nagios as follows...</p>
<p><b>#mkdir /usr/local/nagios</b></p>
<p>Change the owner of the base installtion directory to be the Nagios user and group you added earlier as follows:</p>
<p><b>#chown nagios.nagios /usr/local/nagios</b></p>
<p><b>Identify Web Server User</b></p>
<p>You're  probably going to want to issue external commands (like  acknowledgements and scheduled downtime) from the web interface. To do  so, you need to identify <span class="IL_AD" id="IL_AD12">the user<span class="IL_AD_ICON"></span></span> your web server runs as (typically apache, although this may differ on  your system). This setting is found in your web server configuration  file. The following command can be used to quickly determine what user  Apache is running as (paths may differ on your system):</p>
<p><b>#grep "^User" /etc/httpd/conf/httpd.conf</b></p>
<p><b>Add Command File Group</b></p>
<p>Next we're going to create a new group whose members include the user your web server is running as and the user  Nagios is running as. Let's say we call this new group 'nagcmd' (you  can name it differently if you wish). On RedHat Linux you can use the  following command to add a new group (other systems may differ):</p>
<p><b>#/usr/sbin/groupadd nagcmd</b></p>
<p>Next,  add the users that your web server and Nagios run as to the newly  created group with the following commands (I'll assume apache and nagios  are the respective users):</p>
<p><b>#/usr/sbin/usermod -G nagcmd apache<br />#/usr/sbin/usermod -G nagcmd nagios</b><br /><b><br />Run the Configure Script</b></p>
<p>Run  the configure script to initialize variables and create a Makefile as  follows...(the last two options: --with-command-xxx are optional, but  needed if you want to issue external commands)</p>
<p><b>#./configure  --prefix=prefix --with-cgiurl=cgiurl --with-htmurl=htmurl  --with-nagios-user=someuser --with-nagios-group=somegroup  --with-command-group=cmdgroup</b></p>
<p>    <i>* Replace prefix with the installation directory that you created in the step above (default is /usr/local/nagios)<br />     * Replace cgiurl with the actual url you will be using to access the  CGIs (default is /nagios/cgi-bin). Do NOT append a slash at the end of  the url.<br />    * Replace htmurl with the actual url you will be using  to access the HTML for the main interface and documentation (default is  /nagios/)<br />    * Replace someuser with the name of a user on your  system that will be used for setting permissions on the installed files  (default is nagios)<br />    * Replace somegroup with the name of a group  on your system that will be used for setting permissions on the  installed files (default is nagios)<br />    * Replace cmdgroup with the  name of the group running the web server (default is nagios, in the  example above it was nagcmd). This will allow group members (i.e. your  web server) to be able to submit external commands to Nagios. </i></p>
<p><b>Compile Binaries</b></p>
<p>Compile Nagios and the CGIs with the following command:</p>
<p><b>#make all</b><br /><span style="text-decoration:underline;"><b><br />Installing The Binaries And HTML Files</b></span></p>
<p>Install the binaries and HTML files (documentation and main web page) with the following command:<br /><b><br />#make install</b></p>
<p><b>Installing An Init Script</b></p>
<p>If you wish, you can also install the sample init script to /etc/rc.d/init.d/nagios with the following command:</p>
<p><b>#make install-init</b></p>
<p>You may have to edit the init script to make sense with your particular OS and Nagios installation by editing paths, etc.</p>
<p><b>Directory Structure And File <span class="IL_AD" id="IL_AD10">Locations<span class="IL_AD_ICON"></span></span></b></p>
<p>Change to the root of your Nagios installation directory with the following command...</p>
<p><b>#cd /usr/local/nagios</b></p>
<p>You should see five different subdirectories. A brief description of what each directory contains is given in the table below.</p>
<p><b>Sub-Directory: </b>   Contents<br /><b>bin/: </b>           Nagios core program<br /><b>etc/: </b>   Main, resource, object, and CGI configuration files should be put here<br /><b>sbin/: </b>   CGIs<br /><b>share/: </b>   HTML files (for web interface and online documentation)<br /><b>var/:    </b>        Empty directory for the log file, status file, retention file, etc.<br /><b>var/archives/:</b>  Empty directory for the archived logs<br /><b>var/rw: </b>   Empty directory for the external command file</p>
<p><b>Installing The Plugins</b></p>
<p>In  order for Nagios to be of any use to you, you're going to have to  download and install some plugins. Plugins are usually installed in the  libexec/ directory of your Nagios installation (i.e.  /usr/local/nagios/libexec). Plugins are scripts or binaries which  perform all the service and host checks that constitute monitoring. You  can grab the latest release of the plugins from the Nagios downloads  page or directly from the SourceForge project page.</p>
<p><b>Setup The Web Interface</b></p>
<p>You're  probably going to want to use the web interface, so you'll also have to  read the instructions on setting up the web interface and configuring  web authentication, etc. next.</p>
<p><b><span style="text-decoration:underline;">Configuring Nagios</span></b></p>
<p>So  now you have things compiled and installed, but you still haven't  configured Nagios or defined objects (hosts, services, etc.) that should  be monitored.</p>
<p><a name="more"></a>Adding web authentication for users in nagios </p>
<p>/usr/local/apache/bin/htpasswd /usr/local/nagios/etc/htpasswd.users guest </div>
