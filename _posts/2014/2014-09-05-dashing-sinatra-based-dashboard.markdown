---
layout: post
title: Dashing - Sinatra based dashboard
date: 2014-09-05 04:27:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Dashboard
- ruby
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '3647513220329112444'
---
<div dir="ltr" style="text-align:left;">Being in Ops team, we require Dashboard all the time with lots of metrics , we have quite lots of Ops tool chain in production and each individual tool has its own home page which serves as its own dashboard. E.g.</p>
<p>
<ol style="text-align:left;">
<li><a href="https://mathias-kettner.de/check_mk.html">Check_Mk</a></li>
<li><a href="http://jenkins-ci.org/">Jenkins</a></li>
<li><a href="http://ganglia.sourceforge.net/">Ganglia</a></li>
<li><a href="http://memcached.org/">Memcached</a></li>
<li><a href="http://www.mysql.com/">Mysql</a> </li>
<li><a href="http://graphite.wikidot.com/">graphite</a></li>
<li>and lots of custom metrics dashboard built in PHP </li>
</ol>
<div>But we wanted a single unified Dashbord which level 1 team can watch infact presented on TV screen so that any one in the team can have glance of it. The dashboard should be simple and catchy so that the metrics can be easily seen.</div>
<div></div>
<div>Enter <a href="http://dashing.io/">Dashing</a> </div>
<div></div>
<p>
<div style="color:#222222;font-family:sans-serif;font-size:16px;line-height:22.39999961853px;margin-bottom:10px;margin-top:10px;">Dashing is a Sinatra based framework that lets you build beautiful dashboards.</div>
<blockquote class="tr_bq"><div style="color:#222222;font-family:sans-serif;font-size:16px;line-height:22.39999961853px;margin-bottom:10px;margin-top:10px;">Check out a demo over <a href="http://dashingdemo.herokuapp.com/sample" style="color:#444444;" target="_blank">here</a>. <a href="http://dashingdemo.herokuapp.com/sampletv" style="color:#444444;" target="_blank">Here's another one</a>, optimized for 1080p screens.</div>
<div style="color:#222222;font-family:sans-serif;font-size:16px;line-height:22.39999961853px;margin-bottom:10px;margin-top:10px;"><strong>Key features:</strong></div>
<ul style="color:#222222;font-family:sans-serif;font-size:16px;line-height:22.39999961853px;margin:1em 0;padding:0 0 0 40px;">
<li>Use premade widgets, or fully create your own with scss, html, and coffeescript.</li>
<li>Widgets harness the power of data bindings to keep things DRY and simple. Powered by <a href="http://batmanjs.org/" style="color:#444444;" target="_blank">batman.js</a>.</li>
<li>Use the API to push data to your dashboards, or make use of a simple ruby DSL for fetching data.</li>
<li>Drag &amp; Drop interface for re-arranging your widgets.</li>
<li><a href="https://github.com/Shopify/dashing/wiki/How-to%3A-Deploy-to-Heroku" style="color:#444444;" target="_blank">Host your dashboards on Heroku</a> in less than 30 seconds.</li>
</ul>
<div style="color:#222222;font-family:sans-serif;font-size:16px;line-height:22.39999961853px;margin-bottom:10px;margin-top:10px;"></div>
<div style="color:#222222;font-family:sans-serif;font-size:16px;line-height:22.39999961853px;margin-bottom:10px;margin-top:10px;">This project was created at <a href="http://shopify.com/" style="color:#444444;" target="_blank">Shopify</a> for displaying custom dashboards on TVs around the office.</div>
</blockquote>
<p>Dashing is pretty simple to setup ( check their web site ) but the real power is its widgets which can be easily extented to any level and lots of <a href="https://github.com/Shopify/dashing/wiki/Additional-Widgets">Additional-Widgets</a> are also available.</p>
<p>I have easily set up few dashboard's in Dashing , the cool thing is the data can be made available to widgets either push or pull way. So if you something already setup to collect the metrics you can just push the data to Dashing widget and easily seen in Dashboard.</p>
<p></div>
