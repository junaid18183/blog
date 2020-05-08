---
layout: post
title: 'NRPE: Unable to read output'
date: 2012-09-14 15:47:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Nagios
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '1281784499552614488'
---
<div dir="ltr" style="text-align:left;">In my recent assignment I wanted to monitor the contents of a particular file and basis on that contents Nagios should send an alert. Pretty straight forward job :)</p>
<p>But there was a catch !!! the file that I wanted to monitor is actually owned by root user.</p>
<p>So my custom written plugin  was working very well when I am running manually (using root user ) but failing  when nagios was trying to run it via NRPE it was not working.</p>
<p><b>Solution </b>:   Use Sudo to run the custom plugin , so that when NRPE tries to execute the script it is actually running as a root user.</p>
<p>For that , add a very restrictive entry in sudoers file , giving access to the Nagios user only for that single command as below,</p>
<blockquote class="tr_bq"><div class="MsoNormal" style="margin:0 0 10pt;"><i><span><span style="font-size:small;"><span style="font-family:Calibri;">nagios  ALL=(ALL) NOPASSWD:  /usr/local/nagios/libexec/check_my_file</span></span></span></i></div>
</blockquote>
<p>and in the nrpe.cfg use sudo to run the command , as shown below</p>
<div class="MsoListParagraphCxSpMiddle" style="margin:0 0 0 .5in;"><!--[if gte mso 9]&gt;    &lt;![endif]--></div>
<div class="MsoListParagraphCxSpMiddle" style="margin:0 0 0 .5in;"><!--[if gte mso 9]&gt;   Normal  0          false  false  false    EN-US  X-NONE  X-NONE                                                                    &lt;![endif]--><!--[if gte mso 9]&gt;                                                                                                                                                                                                                                                                                    &lt;![endif]--><!--[if gte mso 10]&gt; /* Style Definitions */  table.MsoNormalTable  {mso-style-name:"Table Normal";  mso-tstyle-rowband-size:0;  mso-tstyle-colband-size:0;  mso-style-noshow:yes;  mso-style-priority:99;  mso-style-parent:"";  mso-padding-alt:0in 5.4pt 0in 5.4pt;  mso-para-margin:0in;  mso-para-margin-bottom:.0001pt;  mso-pagination:widow-orphan;  font-size:11.0pt;  font-family:"Calibri","sans-serif";  mso-ascii-font-family:Calibri;  mso-ascii-theme-font:minor-latin;  mso-hansi-font-family:Calibri;  mso-hansi-theme-font:minor-latin;  mso-bidi-font-family:"Times New Roman";  mso-bidi-theme-font:minor-bidi;} &lt;![endif]--> </div>
<blockquote class="tr_bq"><div class="MsoNormal">command[check_my_file]=sudo /usr/local/nagios/libexec/check_my_file</div>
</blockquote>
<p>and its done :)</p>
<p><b>Note </b>:  On Centos and Redhat Machines you also need to turn off the requiretty option in your suoders file</p>
<p>Comment out the line,</p>
<blockquote class="tr_bq"><p><code>#Defaults    requiretty</code></p></blockquote>
<div class="MsoListParagraphCxSpMiddle" style="margin:0 0 0 .5in;"> </div>
</div>
