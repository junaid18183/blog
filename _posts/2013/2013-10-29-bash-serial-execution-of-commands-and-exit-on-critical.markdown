---
layout: post
title: Bash serial execution of commands and exit on critical
date: 2013-10-29 12:40:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Shell Script
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '4269352220491877511'
---
<div dir="ltr" style="text-align:left;">If you want  to executue the shell commands serially in bash script but also want to keep checking and exit if  any of the command fails</p>
<p>set this at the top of your script</p>
<p>set -e<br />set -o pipefail</div>
