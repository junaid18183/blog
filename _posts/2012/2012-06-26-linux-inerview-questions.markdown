---
layout: post
title: Linux Inerview Questions
date: 2012-06-26 12:42:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '3383258645620976652'
---
<div dir="ltr" style="text-align:left;">1) Difference between setuid and sticky bit in linux?</p>
<p>Set UID:  When a Set UID bit is turned on for a program, your EUID (effective user  ID) becomes the same as the program’s owner when you run the program.  You also gain all the <span class="IL_AD" id="IL_AD1">privileges<span class="IL_AD_ICON"></span></span> of the program’s owner. In other words, if user freddie runs a Set UID program owned by user root, freddie has superuser privileges  while that program is running. Set UID affects programs only; it’s  really not important for data files and directories. If you find a Set  UID program, read the WARNING!!!</p>
<p>Warning: Set UID programs are potentially dangerous.Users can gain extra privileges by using files that grant them superuser privileges.</p>
<p>Set GID: The Set GID bit works similarly to Set UID — anyone running the program gains all the privileges  of the group. When the Set GID box is checked for a directory, the  files in that directory belong to that group regardless of who puts the  files in the directory.</p>
<p>Sticky bit: Checking the Sticky box  affects directories only. If this box is checked, you can’t remove (or  rename) a file in that directory unless you’re the file owner.</p>
<p>2) What is SSH and SSL?</p>
<p>Ans: SSL stands for "<span class="IL_AD" id="IL_AD9">Secure Sockets Layer<span class="IL_AD_ICON"></span></span>".  It commonly uses port 443 to connect your computer to a secure server  on the Internet. SSL is most often used for transmitting <span class="IL_AD" id="IL_AD2">credit card<span class="IL_AD_ICON"></span></span>, tax, banking, or personal information to a business server <span class="IL_AD" id="IL_AD10">somewhere<span class="IL_AD_ICON"></span></span>.  Examples of SSL: you are purchasing a DVD from Amazon.com, you are  filing your taxes online, or you are transferring funds between your  checking and <span class="IL_AD" id="IL_AD12">savings accounts<span class="IL_AD_ICON"></span></span>.</p>
<p>SSH  stands for "Secure Shell". SSH commonly uses port 22 to connect your  computer to another computer on the Internet. It is most often used by  network administrators as a remote login / remote control way to manage  their business servers. Examples would be: your email administrator  needs to reboot the company email server from his home, or your <span class="IL_AD" id="IL_AD11">network administrator<span class="IL_AD_ICON"></span></span> needs to reset your office password while she is away at a conference.</p>
<p>Both  SSL and SSH strive to create confidential connections across the Net.  With only a very few exceptions, it is not possible for a regular hacker  to break into an SSL or SSH connection...the encryption technology is  as reliable as 21st century programming can make it.</p>
<p>When you are  trying to transmit financial information or internal business  documentation, it is highly advisable that you only do so with an SSL or  SSH type of connection.</p>
<p>Both SSL and SSH are special encryption  and protocol technologies used to connect two computers. SSL and SSH  lock out eavesdroppers by encrypting (ciphering) the connection, and <span class="IL_AD" id="IL_AD6">scrambling<span class="IL_AD_ICON"></span></span> the transmitted data so it is meaningless to anyone outside of the two computers.</p>
<p>3) What is Daemon for DNS?</p>
<p>Ans: Named</p>
<p>4) Which is the configuration file for apache server?</p>
<p>/etc/httpd/config/httpd.cconf</p>
<p>5) How to check kernel version?</p>
<p>uname -r</p>
<p>6) How to check Linux version ?</p>
<p>uname  -a is a linux command that will output useful information about your  linux distribution, kernel version, cpu information and more.</p>
<p>cat /etc/linux-release</p>
<p>7) How to check --hardware-platform (arch)</p>
<p>cat /proc/cpuinfo<br /> How to change password of root ?</p>
<p>from single use mode</p>
<p>9) In Linux which password inscription is used ?</p>
<p>MD5</p>
<p>10) what is boot loader?</p>
<p>Bootloader is a piece of code that runs before any operating system is running.</p>
<p>Bootloader are used to boot other operating systems, usually each operating system has a set of bootloaders specific for it.</p>
<p>Bootloaders  usually contain several ways to boot the OS kernel and also contain  commands for debugging and/or modifying the kernel environment.</p>
<p>In this talk we will concentrate on Linux bootloaders.</p>
<p>Since it is usually the first software to run after powerup or reset, it is highly processor and board specific.</p>
<p>11) How to Remount file system</p>
<p>mount -o remount,rw </p>
<p><a name="more"></a> few more</p>
<ul style="text-align:left;">
<li>How do you take a single line of input from <span class="IL_AD" id="IL_AD5">the user<span class="IL_AD_ICON"></span></span> in a shell script?</li>
<li>Write a script to convert all DOS style backslashes to UNIX style slashes in a list of files.</li>
<li>Write a regular expression (or sed script) to replace all occurrences  of the letter ‘f’, followed by any number of characters, followed by  the letter ‘a’, followed by one or more numeric characters, followed by  the letter ‘n’, and replace what’s found with the string “UNIX”.</li>
<li>Write a script to list all the differences between two directories.</li>
<li>Write a program in any language you choose, to reverse a file.</li>
<li>What are the fields of the password file?</li>
<li>What does a plus at the beginning of a line in the password file signify?</li>
<li>Using the man pages, find the correct ioctl to send console output to an arbitrary pty.</li>
<li>What is an MX record?</li>
<li>What is <span class="IL_AD" id="IL_AD8">the prom<span class="IL_AD_ICON"></span></span> command on a Sun that shows the SCSI devices?</li>
<li>What is the factory default SCSI target for /dev/sd0?</li>
<li>Where is that value controlled?</li>
<li>What happens to a child process that dies and has no parent process to wait for it and what’s bad about this?</li>
<li>What’s wrong with sendmail? What would you fix?</li>
<li>What command do you run to check file system consistency?</li>
<li>What’s wrong with running shutdown on a network?</li>
<li>What can be wrong with setuid scripts?</li>
<li>What value does spawn return?</li>
<li> Write a script to send mail from three other machines on <span class="IL_AD" id="IL_AD7">the network<span class="IL_AD_ICON"></span></span> to root at the machine you’re on. Use a ‘here doc’, but include in the  mail message the name of the machine the mail is sent from and the disk  utilization statistics on each machine?</li>
<li>Why can’t root just cd to  someone’s home directory and run a program called a.out sitting there  by typing “a.out”, and why is this good?</li>
<li>What is the difference between UDP and TCP?</li>
<li>What is DNS?</li>
<li>What does nslookup do? </li>
<li>How do you create a swapfile?</li>
<li>How would you check the route table on a workstation/server?</li>
<li>How do you find which ypmaster you are bound to? </li>
<li>How do you fix a problem where a printer will cutoff anything over 1MB?</li>
<li>What is the largest file system size in solaris? SunOS?</li>
<li> What are the different <span class="IL_AD" id="IL_AD4">RAID levels<span class="IL_AD_ICON"></span></span>?</li>
</ul>
<p></div>
