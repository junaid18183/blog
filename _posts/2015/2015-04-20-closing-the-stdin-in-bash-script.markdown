---
layout: post
title: Closing the stdin in Bash script
date: 2015-04-20 14:42:57.000000000 +05:30
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories: []
tags: []
meta:
  _publicize_pending: '1'
---
<p>For one of my requirement my script is behaving oddly and the reason come out was its stdin was open ( will right in detail later)</p>
<p>&nbsp;</p>
<p>to fix the issue I need to close the stdin</p>
<p>reference - http://superuser.com/a/364519/439394</p>
<p>&nbsp;</p>
<p>Closing File Descriptors</p>
<p>n&lt;&amp;-</p>
<p>Close input file descriptor n.</p>
<p>0&lt;&amp;-, &lt;&amp;-</p>
<p>Close stdin.</p>
<p>n&gt;&amp;-</p>
<p>Close output file descriptor n.</p>
<p>1&gt;&amp;-, &gt;&amp;-</p>
<p>Close stdout.</p>
<p>Bas</p>
