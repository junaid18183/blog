---
layout: post
title: Configuring Nagios plugin for Mozilla Firefox
date: 2012-06-26 13:32:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '5324802582606182437'
---
<div dir="ltr" style="text-align:left;">Nagios plugin for Mozilla Firefox Provides <span class="IL_AD" id="IL_AD1">the status<span class="IL_AD_ICON"></span></span> report of your Nagios server in the status bar of Browser.<br />It is really a cool <span class="IL_AD" id="IL_AD5">plug-in<span class="IL_AD_ICON"></span></span> for any one who is using Nagios as its <span class="IL_AD" id="IL_AD6">RIM<span class="IL_AD_ICON"></span></span> tool. </p>
<p>To configure it; first you need to 
<ul style="margin-bottom:0;margin-top:0;">
<li><span class="IL_AD" id="IL_AD7">install<span class="IL_AD_ICON"></span></span> the nagios plugin from  https://addons.mozilla.org/en-US/firefox/addon/3607  (https://addons.mozilla.org/en-US/firefox/addon/3607)</li>
<li>After you install the plugin ,restart the Firefox, then enable this plug in preferences panel. You do this by going to Tools, then to Add-ons.</li>
<li>In setting tab of the plug <span class="IL_AD" id="IL_AD2">in select<span class="IL_AD_ICON"></span></span> add new connection </li>
<li>Name the connection whatever you would like to</li>
<li>For the “Nagios web interface url” enter the URL of your Nagios web page, provide the authentication so that Plug in can <span class="IL_AD" id="IL_AD8">download<span class="IL_AD_ICON"></span></span> the status data from nagios server</li>
<li>For  the “Status Script url” enter the URL of your status script; If you  have not moved or renamed the cgi-bin that nagios uses then <br />the default path is http://yourdomain.com/nagios/cgi-bin/status.cgi]http://yourdomain.com/nagios/cgi-bin/status.cgi</li>
<li>And save these settings. </li>
</ul>
<p>Enjoy watching your status of servers in your browser window.</div>
