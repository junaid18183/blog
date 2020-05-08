---
layout: post
title: Mysql Database Backup script
date: 2012-06-26 14:42:00.000000000 +05:30
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
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '275089317292127981'
---
<div dir="ltr" style="text-align:left;">Create a file called database_backup.sh and also an empty directory called mysql_backup. </p>
<p>The database_backup.sh script should have the following info :</p>
<p>
<pre style="display:inline;margin-top:0;">#!/bin/sh <br />date=`date '+%m-%d-%y'`</pre>
<pre style="display:inline;margin-top:0;">PATH="~/mysql_backup/database_name.$date"<br /></pre>
<pre style="display:inline;margin-top:0;">mysqldump -u database_username -pdatabase_password database_name &gt; $PATH</pre>
<p>
<div class="codeheader"><span class="IL_AD" id="IL_AD4"><br /></span></div>
<p>Run the script that performs the backup job.</p>
<p>Using Cron  :</p>
<p>Set  this script up to run every night, etc. as a cron job. It will save an  sql dump of your database every night in the mysql_backup.<br />e.g </p>
<p>* 23 * * * your_userid /path/to/backup/script</p></div>
