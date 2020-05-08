---
layout: post
title: Installing Nagios and Munin
date: 2012-06-26 13:44:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '4095359541456759699'
---
<div dir="ltr" style="text-align:left;">Login to Nagios server (where you want to <span class="IL_AD" id="IL_AD3">install<span class="IL_AD_ICON"></span></span> Nagios Server)</p>
<p>*************************************<br />Apache Instalation </p>
<p>sudo <span class="IL_AD" id="IL_AD11">apt-get<span class="IL_AD_ICON"></span></span> install apache2</p>
<p>sudo apt-get install libapache2-mod-php5</p>
<p>sudo apt-get install build-essential</p>
<p>sudo apt-get install libgd2-xpm-dev</p>
<p>****************************************</p>
<p>Create Account Information</p>
<p>Become the root user.</p>
<p>sudo -s</p>
<p>Password123</p>
<p>Create a new nagios <span class="IL_AD" id="IL_AD4">user account<span class="IL_AD_ICON"></span></span> and give it a password.</p>
<p>/usr/sbin/useradd -m -s /bin/bash nagios</p>
<p>passwd nagios</p>
<p>Enter new UNIX password:nagiosadmin<br />Retype new UNIX password:nagiosadmin<br />passwd: password updated successfully</p>
<p>root@stg-monitor:~# /usr/sbin/groupadd nagcmd<br />root@stg-monitor:~# /usr/sbin/usermod -a -G nagcmd nagios<br />root@stg-monitor:~# /usr/sbin/usermod -a -G nagcmd www-data</p>
<p>**************************************************</p>
<p><span class="IL_AD" id="IL_AD5">Download<span class="IL_AD_ICON"></span></span> the tar ball for Nagios and Nagios Plugins</p>
<p>****************************************************</p>
<p>Configure </p>
<p>./configure --with-command-group=nagcmd</p>
<p>*** Configuration <span class="IL_AD" id="IL_AD7">summary<span class="IL_AD_ICON"></span></span> for nagios 3.2.3 10-03-2010 ***:</p>
<p> General Options:<br /> -------------------------<br />        Nagios executable:  nagios<br />        Nagios user/group:  nagios,nagios<br />       Command user/group:  nagios,nagcmd<br />            Embedded Perl:  no<br />             Event Broker:  yes<br />        Install ${prefix}:  /usr/local/nagios<br />                Lock file:  ${prefix}/var/nagios.lock<br />   <span class="IL_AD" id="IL_AD1">Check result<span class="IL_AD_ICON"></span></span> directory:  ${prefix}/var/spool/checkresults<br />           Init directory:  /etc/init.d<br />  Apache conf.d directory:  /etc/apache2/conf.d<br />             <span class="IL_AD" id="IL_AD6">Mail program<span class="IL_AD_ICON"></span></span>:  /bin/mail<br />                  Host OS:  linux-gnu</p>
<p> Web Interface Options:<br /> ------------------------<br />                 HTML URL:  http://<span class="IL_AD" id="IL_AD12">localhost<span class="IL_AD_ICON"></span></span>/nagios/<br />                  CGI URL:  http://localhost/nagios/cgi-bin/<br /> Traceroute (used by WAP):</p>
<p>Review the options above for accuracy.  If they look okay,<br />type 'make all' to compile the main program and CGIs.</p>
<p>*************************************************************</p>
<p>Compile the Nagios <span class="IL_AD" id="IL_AD8">source code<span class="IL_AD_ICON"></span></span>. </p>
<p>make all</p>
<p>*************************************************************</p>
<p>Install binaries, init script, sample config files and set permissions on the external command directory.</p>
<p>make install</p>
<p>make install-init</p>
<p>make install-config</p>
<p>make install-commandmode</p>
<p>*************************************************************</p>
<p>Configure the Web Interface</p>
<p>Install the Nagios web config file in the Apache conf.d directory.</p>
<p>make install-webconf</p>
<p>Create  a nagiosadmin account for logging into the Nagios web interface.  Remember the password you assign to this account - you'll need it later.</p>
<p>htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin</p>
<p><span class="IL_AD" id="IL_AD2">New password<span class="IL_AD_ICON"></span></span>:nagios<br />Re-type new password:nagios</p>
<p>Restart Apache to make the new settings take effect.</p>
<p>/etc/init.d/apache2 reload</p>
<p>*************************************************************</p>
<p>Compile and Install the Nagios Plugins</p>
<p>cd /home/cybage/untar/nagios-plugins-1.4.11</p>
<p>./configure --with-nagios-user=nagios --with-nagios-group=nagios</p>
<p>make</p>
<p>make install</p>
<p>*************************************************************</p>
<p>Configure Nagios to automatically start when the system boots.</p>
<p>ln -s /etc/init.d/nagios /etc/rcS.d/S99nagios</p>
<p>Verify the sample Nagios configuration files.</p>
<p>/usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg</p>
<p>If there are no errors, start Nagios.</p>
<p>/etc/init.d/nagios start</p>
<p>*************************************************************</p>
<p>Check Nagios web interface at </p>
<p>http://monitor.dimestore.com/nagios/</p>
<p>*************************************************************</p>
<p>Configure NRPE plugins on PROD-Monitor server</p>
<p>NRPE require you install xinetd and libssl-dev so we’ll do that now</p>
<p>apt-get install xinetd<br />apt-get install libssl-dev</p>
<p>/home/cybage/untar/nrpe-2.12</p>
<p>make all<br />make install-plugin<br />make install-daemon<br />make install-daemon-config<br />make install-xinetd</p>
<p>now  we need to configure the daemon so it will talk to our Nagios server,  well do this buy editing /etc/xinetd.d/nrpe and adding our monitoring  servers address: </p>
<p>only_from       = ??.??.??.??</p>
<p>Then add “nrpe 5666/tcp # NRPE” to /etc/services as below </p>
<p>nrpe            5666/tcp                        # NRPE</p>
<p>Restart xinetd services </p>
<p>root@prod-monitor:~/untar/nrpe-2.12# /etc/init.d/xinetd restart<br /> *  Stopping internet superserver xinetd                                                                                                                 [ OK ]<br /> * Starting internet superserver xinetd                                                                                                                 [ OK ]</p>
<p>Confirm NRPE is listening on port 5666</p>
<p>root@prod-monitor:~/untar/nrpe-2.12# netstat -at | grep nrpe<br />tcp        0      0 *:nrpe                  *:*                     LISTEN</p>
<p>Confirm check_nrpe is present in the Nagios libexec folder </p>
<p>ls -l /usr/local/nagios/libexec/check_nrpe</p>
<p>****************************************************************************</p>
<p>edit Nagios configuration to replace the localhost with actual nagios host name and new required cfg files</p>
<p>cd /usr/local/nagios/etc/<span class="IL_AD" id="IL_AD9">objects<span class="IL_AD_ICON"></span></span>/</p>
<p>sudo touch hosts.cfg services.cfg hostgroups.cfg</p>
<p>edit nagios.cfg so that nagios can use these newly added configuration files </p>
<p>and comment the localhosts.cfg file </p>
<p>cfg_file=/usr/local/nagios/etc/objects/hosts.cfg<br />cfg_file=/usr/local/nagios/etc/objects/hostgroups.cfg<br />cfg_file=/usr/local/nagios/etc/objects/contactgroups.cfg<br />cfg_file=/usr/local/nagios/etc/objects/services.cfg</p>
<p>Verify the sample Nagios configuration files.</p>
<p>/usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg</p>
<p>If there are no errors, reload Nagios.</p>
<p>sudo /etc/init.d/nagios reload</p>
<p>****************************************************************************</p>
<p>Installing Munin and munin node </p>
<p>sudo apt-get install munin munin-node</p>
<p>edit munin.conf file and replace localhost with proper name </p>
<p>[prod-monitor]<br />    address ??.??.??.??<br />    use_node_name yes</p>
<p>and update the Munin server </p>
<p>sudo su - munin --shell=/bin/bash  -c /usr/share/munin/munin-update</p>
<p>update munin-node.conf  to add munin servers ip address</p>
<p>allow ^127\.0\.0\.1$<br />allow ^??\.??\.??\.??$</p>
<p>and restart munin node </p>
<p>sudo service munin-node restart</p>
<p>****************************************************************************</p>
<p>Add munin nodes in munin.conf</p>
<p>Restart Munin <br />sudo su - munin --shell=/bin/bash -c /usr/share/munin/munin-update</p>
<p>***********************************************************************************</p>
<p>Add entries in hosts.cfg<br />Add entries in hostgroups.cfg</p>
<p>Verify the sample Nagios configuration files.</p>
<p>/usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg</p>
<p>sudo /etc/init.d/nagios reload</p>
<p>***********************************************************************************<br />Add nrpe command in commands.cfg</p>
<p>define command{<br />        command_name check_nrpe<br />        command_line $USER1$/check_nrpe -H $HOSTADDRESS$ -c $ARG1$<br />}</p>
<p>Add NRPE services </div>
