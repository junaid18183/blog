---
layout: post
title: Monitor Failed Jenkins Job
date: 2014-09-05 03:54:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- check_mk
- Cron. Jenkins
- Nagios
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '6592261731113548945'
---
<div dir="ltr" style="text-align:left;">We use Jenkins quite differently :) ( I will write it the use case later ) , And although the Jenkins provides the Email alerting if the Job is unstable. But  in our scenario we wanted an aggregate Job monitoring for the jenkins job so that as soon as any of the Jenkins Job failed our level team got hold of it.</p>
<p>Below is the simple Python plugin I have written  to achieve this. This python script gets all jobs stats using the Jenkins API and then parses for the stability of the Job.   </p></div>
