---
layout: post
title: etsy/logster
date: 2015-06-29 10:16:28.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  _publicize_job_id: '12144663220'
---
<p><a href="https://github.com/etsy/logster">etsy/logster</a>.</p>
<p>&nbsp;</p>
<p style="box-sizing:border-box;margin-top:0;margin-bottom:16px;font-family:'Helvetica Neue', Helvetica, 'Segoe UI', Arial, freesans, sans-serif;line-height:25.60000038147px;">Logster is a utility for reading log files and generating metrics to configurable outputs. Graphite, Ganglia, Amazon CloudWatch, Nagios, StatsD and stdout are currently supported. It is ideal for visualizing trends of events that are occurring in your application/system/error logs. For example, you might use logster to graph the number of occurrences of HTTP response code that appears in your web server logs.</p>
<p style="box-sizing:border-box;margin-top:0;margin-bottom:16px;font-family:'Helvetica Neue', Helvetica, 'Segoe UI', Arial, freesans, sans-serif;line-height:25.60000038147px;">Logster maintains a cursor, via a tailer, on each log file that it reads so that each successive execution only inspects new log entries. In other words, a 1 minute crontab entry for logster would allow you to generate near real-time trends in the configured output for anything you want to measure from your logs.</p>
<p style="box-sizing:border-box;margin-top:0;margin-bottom:16px;font-family:'Helvetica Neue', Helvetica, 'Segoe UI', Arial, freesans, sans-serif;line-height:25.60000038147px;">This tool is made up of a framework script, logster, and parsing scripts that are written to accommodate your specific log format. Sample parsers are included in this distribution. The parser scripts essentially read a log file line by line, apply a regular expression to extract useful data from the lines you are interested in, and then aggregate that data into metrics that will be submitted to the configured output. Take a look through the sample parsers, which should give you some idea of how to get started writing your own.</p>
