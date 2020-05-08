---
layout: post
title: Dropbox commandline
date: 2014-06-11 12:10:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '4574130378326959669'
---
<div dir="ltr" style="text-align:left;">
<div class="MsoNormal">Installation...</div>
<div class="MsoNormal"></div>
<div class="MsoNormal">Take a <b>CentOS 6.x</b> box for a smooth install (the curl on centos 5.x seems buggy/incompatible)</div>
<div class="MsoNormal"></div>
<ul type="disc">
<li class="MsoNormal">As root user, run the 2 commands below</li>
</ul>
<ul type="circle">
<li class="MsoNormal"> </li>
<li class="MsoNormal">curl "<a href="https://raw.github.com/andreafabrizi/Dropbox-Uploader/master/dropbox_uploader.sh">https://raw.github.com/andreafabrizi/Dropbox-Uploader/master/dropbox_uploader.sh</a>"       -o /tmp/dropbox_uploader.sh</li>
<li class="MsoNormal">install       /tmp/dropbox_uploader.sh /usr/local/bin/dropbox_uploader</li>
</ul>
<li class="MsoNormal">dropbox_uploader is installed and can be run by any      user. As root or as any other user... run command</li>
<ul type="circle">
<li class="MsoNormal"> </li>
<li class="MsoNormal">dropbox_uploader</li>
<li class="MsoNormal"><b>Do the instructions as       the script says</b></li>
</ul>
<ul type="square">
<li class="MsoNormal"> </li>
<li class="MsoNormal"> 1) Open the        following URL in your Browser, and log in using your account: <a href="https://www2.dropbox.com/developers/apps">https://www2.dropbox.com/developers/apps</a></li>
<li class="MsoNormal"> 2) Click on        "Create App", then select "Dropbox API app"</li>
<li class="MsoNormal"> 3) Select        "Files and datastores"</li>
<li class="MsoNormal"> 4) Now go on        with the configuration, choosing the app permissions and access        restrictions to your DropBox folder</li>
<li class="MsoNormal"> 5) Enter the        "App Name" that you prefer (e.g. JunedTest)</li>
<li class="MsoNormal"> </li>
<li class="MsoNormal">Now, click on the        "Create App" button.</li>
<li class="MsoNormal"> When your new        App is successfully created, please COPY the, App Key, App Secret and        the Permission type shown in the confirmation page</li>
<li class="MsoNormal">Asks you to confirm by        going to a URL like <a href="https://www2.dropbox.com/1/oauth/authorize?oauth_token=%3CSOMETOKEN%3E">https://www2.dropbox.com/1/oauth/authorize?oauth_token=</a>,        click ALLOW</li>
<li class="MsoNormal">It saves your info (in        the file .dropbox_uploader)</li>
<li class="MsoNormal">Run        "dropbox_uploader" which prints all commands</li>
</ul>
<div class="MsoNormal"></div>
<div class="MsoNormal">To remove the credentials, remove the file <b>.dropbox_uploader</b> in your home dir.</div>
<p>
<div class="MsoNormal">Remove /usr/local/bin/dropbox_uploader if u no longer need it.</div>
</div>
