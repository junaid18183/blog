---
layout: post
title: Script for File Details in your current Directory
date: 2012-06-25 12:40:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '6927433066032156853'
---
<div dir="ltr" style="text-align:left;">using this Script you can see  File Details in your current Directory </p>
<p><span>#!/bin/bash</span><br /><span>echo "No of files in current in Directory"</span><br /><span>ls -l | grep ^- | wc -l</span></p>
<p><span>echo "and there detail are  as follows"</span><br /><span>#echo " File name No of lines word Characters"</span><br /><span>for j in `ls -l | grep ^- | awk '{print $9}'`</span><br /><span>do</span><br /><span>wc  -lmw $j | awk '{print  "File name is"" "$4"\t""No Of lines  in that  file"" " $1"\t" "No Of Words in that file" " " $2 "\t" "No of Character  in files"" "$3  }'</span><br /><span>done</span></p>
<blockquote class="tr_bq"><p><b><span class="IL_AD" id="IL_AD9">If you are<span class="IL_AD_ICON"></span></span> using Ubuntu linux make change in file  for j in `ls -l | grep ^- | awk '{print $8}'`</b></p></blockquote>
</div>
