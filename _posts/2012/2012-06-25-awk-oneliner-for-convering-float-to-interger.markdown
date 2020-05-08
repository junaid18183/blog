---
layout: post
title: Awk oneliner for convering float to interger
date: 2012-06-25 12:27:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '6519355966349362089'
---
<div dir="ltr" style="text-align:left;">
<div>echo  2.52690284 | awk '{printf "%.0f",$1}'</p>
<p>if in bash script </p>
<p>$SPEED="3.2"</p>
<p>SPEED=$(echo $SPEED | awk '{printf "%.0f",$1}')</p>
<p>echo $SPEED</p></div>
</div>
