---
layout: post
title: TRIMMIG IN MYSQL
date: 2012-06-26 14:37:00.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Mysql
tags: []
meta:
  blogger_blog: ijuned.blogspot.com
  blogger_7553295648c4d8ebded8b8484926da00_permalink: '4474496690969556462'
---
<div dir="ltr" style="text-align:left;">Some time back I got stuck at the point in Mysql task ,I wanted to trip a part of already existing column in table and then <span class="IL_AD" id="IL_AD7">insert into<span class="IL_AD_ICON"></span></span> other column.</p>
<p><span class="IL_AD" id="IL_AD6">Reference<span class="IL_AD_ICON"></span></span> is the column that contains the <span class="IL_AD" id="IL_AD1">Reference number<span class="IL_AD_ICON"></span></span> e.g. '090216-000016'<br />RDate is the column is which stores <span class="IL_AD" id="IL_AD4">the date<span class="IL_AD_ICON"></span></span> of the reference,  and first part of Reference contains the date. So I wanted to trip the Reference number to get the data for RDate column.</p>
<p>Here is how I did it,</p>
<p>mysql&gt; select Reference from RNS  where Reference='090216-000016';<br />+---------------+<br />| Reference     |<br />+---------------+<br />| 090216-000016 |<br />+---------------+<br />1 row in set (0.00 sec)</p>
<p>mysql&gt; select LEFT (Reference,6) from RNS  where Reference='090216-000016';<br />+--------------------+<br />| LEFT (Reference,6) |<br />+--------------------+<br />| 090216             |<br />+--------------------+<br />1 row in set (0.01 sec)</p>
<p>mysql&gt; update RNS set RDATE=LEFT(Reference,6) where Reference='090205-000154';<br />Query OK, 1 row affected (0.00 sec)<br />Rows matched: 1  Changed: 1  Warnings: 0</p>
<p>mysql&gt; select Reference,RDATE from RNS  where Reference='090205-000154';<br />+---------------+------------+<br />| Reference     | RDATE      |<br />+---------------+------------+<br />| 090205-000154 | 2009-02-05 |<br />+---------------+------------+</p>
<p>Hope it will be useful.</p></div>
