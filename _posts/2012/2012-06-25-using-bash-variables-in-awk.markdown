---
layout: post
title: Using bash variables in awk
date: 2012-06-25 12:41:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '8431914300368371906'
---
<div dir="ltr" style="text-align:left;">
<div>C_DATE=$(cat $1 |grep "Processing" | sed "s/[^0-9]//g" )</p>
<p>cat $1 | awk 'BEGIN {RS="Data"; FS="\n";OFS=":" } {print $1,$5,$8,$9,$10}' | awk  'BEGIN {FS=":";OFS=":"}NR &gt;1 {print <b>$C_DATE</b>,$1,$2,$3+0,"\tTotal Closed",$5+$7,$8,$9+0,"\tClosed%\t",(($5+$7)/$3)*100,"\tError%\t",($9/$3)*100  } </p>
<p>will <span class="IL_AD" id="IL_AD1">not work<span class="IL_AD_ICON"></span></span> </p>
<p>to use Bash variable in AWK you need to redefine the variable in awk using -v </div>
<blockquote class="tr_bq"><p>The option -v <span class="IL_AD" id="IL_AD3">followed<span class="IL_AD_ICON"></span></span> by var=value is an assignment to be  ( AWK MAN PAGE)</p></blockquote>
<div></div>
<div>C_DATE=$(cat $1 |grep "Processing" | sed "s/[^0-9]//g" )</p>
<p>#echo "$C_DATE"</p>
<p>cat  $1 | awk 'BEGIN {RS="Data"; FS="\n";OFS=":" } {print $1,$5,$8,$9,$10}' |  awk -v C_DATE="$C_DATE" 'BEGIN {FS=":";OFS=":"}NR &gt;1 {print  C_DATE,$1,$2,$3+0,"\tTotal  Closed",$5+$7,$8,$9+0,"\tClosed%\t",(($5+$7)/$3)*100,"\tError%\t",($9/$3)*100   } '</p></div>
</div>
