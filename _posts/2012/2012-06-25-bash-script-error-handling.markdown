---
layout: post
title: BASH Script Error Handling
date: 2012-06-25 13:44:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '7239170227007348199'
---
<div dir="ltr" style="text-align:left;">BASH Script Error Handling</p>
<p>You can catch errors returned by your commands in BASH <span class="IL_AD" id="IL_AD1">shell scripts<span class="IL_AD_ICON"></span></span> with "$?". In this example we will do a backup rsync of our home directories to our <span class="IL_AD" id="IL_AD3">file server<span class="IL_AD_ICON"></span></span>.  If a program gives anything but a zero return code, there has been an  error of some type. With this method, any non-zero return codes will be  reported, along with the output from the previous command.</p>
<p>#!/bin/bash<br />SRCDIR="/home"<br />BACKUPDIR="fileserver:/home_backup"<br />CMD=`rsync -aq --partial --delete "$SRCDIR" "$BACKUPDIR"`<br />if [ $? != 0 ]; then<br />{<br />    <span class="IL_AD" id="IL_AD6">echo<span class="IL_AD_ICON"></span></span> "BACKUP ERROR: problem syncing $SRCDIR to $BACKUPDIR"</p>
<p>    echo $CMD<br />    exit 1<br />} fi</p>
<p>This  script will run silently, unless there is an error. We could then call  this script daily from cron, mailing any error output to root:<br /># <span class="IL_AD" id="IL_AD2">crontab<span class="IL_AD_ICON"></span></span> -e</p>
<p># daily home backup<br />0 4 * * * /root/bin/backup.sh</div>
