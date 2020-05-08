---
layout: post
title: awk summing coloumn values
date: 2012-06-25 12:38:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '1527494030554733358'
---
<div dir="ltr" style="text-align:left;">
<div>I got lines in <span class="IL_AD" id="IL_AD10">format<span class="IL_AD_ICON"></span></span> </div>
<div></div>
<blockquote class="tr_bq"><p>juned_workers 0.03322<br />juned_workers 0<br />juned_workers 0.17053<br />juned_workers 0<br />juned_workers 0.41322<br />juned_workers 0<br />juned_workers 0.16864<br />juned_workers 0.05603<br />juned_workers 0<br />juned_workers 0.15836 </p></blockquote>
<div></div>
<div>The output I required was in format  </div>
<blockquote class="tr_bq"><p>Row1 juned_workers 0.03322<br />Row2 juned_workers 0<br />Row3 juned_workers 0.17053<br />Row4 juned_workers 0<br />Row5 juned_workers 0.41322<br />Row6 juned_workers 0<br />Row7 juned_workers 0.16864<br />Row8 juned_workers 0.05603<br />Row9 juned_workers 0<br />Row10 juned_workers 0.15836<br />Total :  1</p></blockquote>
<div></div>
<div></div>
<div><i>cat juned.txt |  awk '{print "Row"NR,$_} { s += $2 } END { print "Total : ", s} '</i> </div>
</div>
