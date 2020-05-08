---
layout: post
title: Conditional variable assignment/ substitution
date: 2012-11-16 14:27:00.000000000 +05:30
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
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '3830092061976340722'
---
<div dir="ltr" style="text-align:left;">
<div class="MsoNormal">Bash does support the conditional variable assignment/ substitution e.g.  below code snippet </div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><span>#! /bin/bash</span></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><span>name=${2:-"Juned"}</span></div>
<div class="MsoNormal"></div>
<div class="MsoNormal"><span>if [ "$name" != "Juned" ];then</span></div>
<div class="MsoNormal"><span>echo  "hello $name"</span></div>
<div class="MsoNormal"><span>else</span></div>
<div class="MsoNormal"><span>echo "bye"</span></div>
<div class="MsoNormal"><span>fi</span></div>
<div class="MsoNormal"></div>
<div class="MsoNormal">will define the variable name with second command line parameter , but if there is no second command line parameter then the name is defaulted to Juned</div>
</div>
