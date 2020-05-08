---
layout: post
title: Backing Up MySQL Database
date: 2012-06-26 14:41:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- backup
- database
- Mysql
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '6686650287235933430'
---
<div dir="ltr" style="text-align:left;">MySQL database backup can be accomplished in two ways:</p>
<p>a) Copying the raw mysql database files &amp;<br />b) <span class="IL_AD" id="IL_AD6">Exporting<span class="IL_AD_ICON"></span></span> tables to text files</p>
<p><span style="background-color:blue;"><br /></span><br /><b>Copying the Mysql database Files : </b></p>
<p>MySQL  uses the same table format on different platforms, so it's possible to  copy MySQL table and index files from one platform and use them on  another without any <span class="IL_AD" id="IL_AD11">difficulties<span class="IL_AD_ICON"></span></span> (assuming, of course, that you're using the same version of MySQL on both platforms).</p>
<p><span style="background-color:white;"><b>Exporting tables to text files.</b></span></p>
<p>The MySQLDump is handy utility that can be used to quickly backup the MySQL Database to the text files. To use the MySQLDump utility it <span class="IL_AD" id="IL_AD2">is required<span class="IL_AD_ICON"></span></span> to <span class="IL_AD" id="IL_AD8">logon to<span class="IL_AD_ICON"></span></span> the System running the MySQL Databse. You can use <span class="IL_AD" id="IL_AD10">Telnet<span class="IL_AD_ICON"></span></span> to remotely logon to the system if you don't have the physical access to the machine.<br />The syntax for the command is as follows.</p>
<p><i>mysqldump -u [Username] -p [password] [databasename] &gt; [backupfile.sql]</i></p>
<p>[username] - this is your database username<br />[password]- this is the password for your database<br />[databasename] - the name of your database<br />[backupfile.sql] - the filename for your database backup</p>
<p>Let's discuss the example of backing up MySQL Database named "accounts" into text file accounts.sql. Here are the scenarios of taking the backup assuming that both <span class="IL_AD" id="IL_AD3">user name and password<span class="IL_AD_ICON"></span></span> of the database is "admin".</p>
<p><b>a) Taking the full backup of all the tables including the data. </b></p>
<p>Use the following command to accomplish this:<br />mysqldump -u admin -p admin accounts &gt; accounts.sql</p>
<p><b>b) Taking the backup of table <span class="IL_AD" id="IL_AD9">structures<span class="IL_AD_ICON"></span></span> only. </b></p>
<p>Use the following command to accomplish this:<br />mysqldump -u admin -p admin --no-data accounts &gt; accounts.sql</p>
<p><b>c) Taking the backup data only. </b></p>
<p>Use the following command to accomplish this:<br />mysqldump -u admin -p admin --no-create-info accounts &gt; accounts.sql</p>
<p><b>Restoring MySQL Database</b></p>
<p>Restoring the MySQL is very easy job. You can use the following to command to restore the accounts database from accounts.sql <span class="IL_AD" id="IL_AD7">backup file<span class="IL_AD_ICON"></span></span>.</p>
<p><i>mysql - u admin -p admin accounts &lt; accounts.sql</i></p>
<p>In this tutorial you learned how to take the backup of your MySQL Database and restore the same in the event of some database crash or on some other machine.</p></div>
